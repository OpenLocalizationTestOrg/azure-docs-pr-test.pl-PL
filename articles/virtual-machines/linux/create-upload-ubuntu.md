---
title: aaaCreate i przekazywanie dysku VHD Ubuntu Linux na platformie Azure
description: "Dowiedz się toocreate i przekaż Azure wirtualnego dysku twardego (VHD) z systemem operacyjnym Ubuntu Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 3e097959-84fc-4f6a-8cc8-35e087fd1542
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: cc546a487f769b32432a7e80ddcd0f6af44e201f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a><span data-ttu-id="1f050-103">Przygotowywanie maszyny wirtualnej systemu Ubuntu dla platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1f050-103">Prepare an Ubuntu virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a><span data-ttu-id="1f050-104">Obrazy Ubuntu oficjalnego w chmurze</span><span class="sxs-lookup"><span data-stu-id="1f050-104">Official Ubuntu cloud images</span></span>
<span data-ttu-id="1f050-105">Ubuntu teraz publikuje oficjalnego Azure wirtualne dyski twarde do pobrania na [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span><span class="sxs-lookup"><span data-stu-id="1f050-105">Ubuntu now publishes official Azure VHDs for download at [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span></span> <span data-ttu-id="1f050-106">Jeśli konieczne toobuild własne specjalistyczne obrazu Ubuntu na platformie Azure, zamiast hello Procedura ręcznego poniżej jest zalecane toostart z tych znane pracy wirtualne dyski twarde i dostosowywać odpowiednio do potrzeb.</span><span class="sxs-lookup"><span data-stu-id="1f050-106">If you need toobuild your own specialized Ubuntu image for Azure, rather than use hello manual procedure below it is recommended toostart with these known working VHDs and customize as needed.</span></span> <span data-ttu-id="1f050-107">najnowsze wersje obraz powitania zawsze można znaleźć pod hello następujących lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="1f050-107">hello latest image releases can always be found at hello following locations:</span></span>

* <span data-ttu-id="1f050-108">Ubuntu 12.04/dokładne: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="1f050-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="1f050-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="1f050-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="1f050-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="1f050-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f050-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1f050-111">Prerequisites</span></span>
<span data-ttu-id="1f050-112">W tym artykule przyjęto założenie, zainstalowano wirtualnego dysku twardego Ubuntu Linux systemu operacyjnego tooa.</span><span class="sxs-lookup"><span data-stu-id="1f050-112">This article assumes that you have already installed an Ubuntu Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="1f050-113">Wiele narzędzi istnieje toocreate plików VHD, na przykład rozwiązanie wirtualizacji takich jak funkcja Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="1f050-113">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="1f050-114">Aby uzyskać instrukcje, zobacz [instalowanie hello roli funkcji Hyper-V i konfigurowanie maszyny wirtualnej](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="1f050-114">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="1f050-115">**Informacje o instalacji Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="1f050-115">**Ubuntu installation notes**</span></span>

* <span data-ttu-id="1f050-116">Zobacz także [ogólne informacje o instalacji systemu Linux](create-upload-generic.md#general-linux-installation-notes) więcej porad na przygotowanie systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="1f050-116">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="1f050-117">Witaj VHDX format nie jest obsługiwany na platformie Azure, tylko **stały VHD**.</span><span class="sxs-lookup"><span data-stu-id="1f050-117">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="1f050-118">Możesz przekonwertować format tooVHD dysku hello za pomocą Menedżera funkcji Hyper-V lub hello polecenia cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="1f050-118">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="1f050-119">Podczas instalowania systemu Linux hello zaleca się użycie standardowe partycje, a nie LVM (często hello domyślnie wiele instalacji).</span><span class="sxs-lookup"><span data-stu-id="1f050-119">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="1f050-120">Pozwoli to uniknąć konfliktów nazw LVM sklonowany maszyn wirtualnych, zwłaszcza w przypadku, gdy na dysku systemu operacyjnego kiedykolwiek wymaga tooanother toobe dołączony maszyny Wirtualnej do rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="1f050-120">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="1f050-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) może być używany dla dysków z danymi, jeśli preferowane.</span><span class="sxs-lookup"><span data-stu-id="1f050-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="1f050-122">Nie należy konfigurować partycji wymiany na powitania dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="1f050-122">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="1f050-123">agenta systemu Linux Hello może być skonfigurowany toocreate pliku wymiany na powitania zasobów dysku.</span><span class="sxs-lookup"><span data-stu-id="1f050-123">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="1f050-124">Więcej informacji na ten temat można znaleźć w poniższych krokach hello.</span><span class="sxs-lookup"><span data-stu-id="1f050-124">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="1f050-125">Wszystkie wirtualne dyski twarde hello muszą mieć rozmiary, które są wielokrotności 1 MB.</span><span class="sxs-lookup"><span data-stu-id="1f050-125">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="manual-steps"></a><span data-ttu-id="1f050-126">Ręczne</span><span class="sxs-lookup"><span data-stu-id="1f050-126">Manual steps</span></span>
> [!NOTE]
> <span data-ttu-id="1f050-127">Przed podjęciem próby wykonania toocreate własny obraz niestandardowy Ubuntu na platformie Azure, należy rozważyć przy użyciu hello wstępnie skompilowany i przetestować obrazy z [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="1f050-127">Before attempting toocreate your own custom Ubuntu image for Azure, please consider using hello pre-built and tested images from [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) instead.</span></span>
> 
> 

1. <span data-ttu-id="1f050-128">W środkowym okienku hello Menedżera funkcji Hyper-V wybierz maszynę wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="1f050-128">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="1f050-129">Kliknij przycisk **Connect** okna hello tooopen hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1f050-129">Click **Connect** tooopen hello window for hello virtual machine.</span></span>

3. <span data-ttu-id="1f050-130">Zastąp bieżący repozytoria hello w Ubuntu hello obrazu toouse repozytoriów Azure.</span><span class="sxs-lookup"><span data-stu-id="1f050-130">Replace hello current repositories in hello image toouse Ubuntu's Azure repos.</span></span> <span data-ttu-id="1f050-131">kroki Hello się nieco różnić w zależności od wersji Ubuntu hello.</span><span class="sxs-lookup"><span data-stu-id="1f050-131">hello steps vary slightly depending on hello Ubuntu version.</span></span>
   
    <span data-ttu-id="1f050-132">Przed rozpoczęciem edycji `/etc/apt/sources.list`, jest zalecane toomake kopii zapasowej:</span><span class="sxs-lookup"><span data-stu-id="1f050-132">Before editing `/etc/apt/sources.list`, it is recommended toomake a backup:</span></span>
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    <span data-ttu-id="1f050-133">Ubuntu 12.04:</span><span class="sxs-lookup"><span data-stu-id="1f050-133">Ubuntu 12.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="1f050-134">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="1f050-134">Ubuntu 14.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="1f050-135">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="1f050-135">Ubuntu 16.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. <span data-ttu-id="1f050-136">Witaj obrazów Ubuntu Azure teraz następujące hello *włączenie sprzętu* jądra (HWE).</span><span class="sxs-lookup"><span data-stu-id="1f050-136">hello Ubuntu Azure images are now following hello *hardware enablement* (HWE) kernel.</span></span> <span data-ttu-id="1f050-137">Aktualizacja hello systemu operacyjnego toohello najnowsze jądra, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="1f050-137">Update hello operating system toohello latest kernel by running hello following commands:</span></span>

    <span data-ttu-id="1f050-138">Ubuntu 12.04:</span><span class="sxs-lookup"><span data-stu-id="1f050-138">Ubuntu 12.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    <span data-ttu-id="1f050-139">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="1f050-139">Ubuntu 14.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    <span data-ttu-id="1f050-140">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="1f050-140">Ubuntu 16.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    <span data-ttu-id="1f050-141">**Zobacz też:**</span><span class="sxs-lookup"><span data-stu-id="1f050-141">**See also:**</span></span>
    - [<span data-ttu-id="1f050-142">https://Wiki.ubuntu.com/Kernel/LTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="1f050-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [<span data-ttu-id="1f050-143">https://Wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="1f050-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. <span data-ttu-id="1f050-144">Zmodyfikuj hello jądra rozruchu wiersza chodników tooinclude jądra dodatkowych parametrów dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1f050-144">Modify hello kernel boot line for Grub tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="1f050-145">toodo tym Otwórz `/etc/default/grub` w edytorze tekstów, Znajdź hello zmiennej o nazwie `GRUB_CMDLINE_LINUX_DEFAULT` (lub Dodaj ją w razie potrzeby) i dokonać jego edycji hello tooinclude następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="1f050-145">toodo this open `/etc/default/grub` in a text editor, find hello variable called `GRUB_CMDLINE_LINUX_DEFAULT` (or add it if needed) and edit it tooinclude hello following parameters:</span></span>
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    <span data-ttu-id="1f050-146">Zapisz i zamknij plik, a następnie uruchom `sudo update-grub`.</span><span class="sxs-lookup"><span data-stu-id="1f050-146">Save and close this file, and then run `sudo update-grub`.</span></span> <span data-ttu-id="1f050-147">Daje to pewność, że wszystkie komunikaty konsoli są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy technicznej dotyczącej debugowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="1f050-147">This will ensure all console messages are sent toohello first serial port, which can assist Azure technical support with debugging issues.</span></span>

6. <span data-ttu-id="1f050-148">Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu.</span><span class="sxs-lookup"><span data-stu-id="1f050-148">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="1f050-149">Zazwyczaj jest to domyślna hello.</span><span class="sxs-lookup"><span data-stu-id="1f050-149">This is usually hello default.</span></span>

7. <span data-ttu-id="1f050-150">Zainstaluj agenta systemu Linux Azure hello:</span><span class="sxs-lookup"><span data-stu-id="1f050-150">Install hello Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    <span data-ttu-id="1f050-151">Witaj `walinuxagent` pakietu może spowodować usunięcie hello `NetworkManager` i `NetworkManager-gnome` pakiety, jeśli są one zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="1f050-151">hello `walinuxagent` package may remove hello `NetworkManager` and `NetworkManager-gnome` packages, if they are installed.</span></span>

8. <span data-ttu-id="1f050-152">Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="1f050-152">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. <span data-ttu-id="1f050-153">Kliknij przycisk **akcji -> zamykania w dół** w Menedżerze funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="1f050-153">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="1f050-154">Dysk VHD systemu Linux jest teraz gotowy toobe przekazać tooAzure.</span><span class="sxs-lookup"><span data-stu-id="1f050-154">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f050-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1f050-155">Next steps</span></span>
<span data-ttu-id="1f050-156">Użytkownik jest teraz gotowy toouse Ubuntu Linux wirtualnego dysku twardego toocreate nowych maszyn wirtualnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="1f050-156">You're now ready toouse your Ubuntu Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="1f050-157">Jeśli hello jest przesyłana tooAzure pliku VHD powitania po raz pierwszy, zobacz kroki 2 i 3 w [tworzenie i przekazywanie wirtualnego dysku twardego, który zawiera system operacyjny Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1f050-157">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="references"></a><span data-ttu-id="1f050-158">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="1f050-158">References</span></span>
<span data-ttu-id="1f050-159">Ubuntu jądra (HWE) na włączenie sprzętu:</span><span class="sxs-lookup"><span data-stu-id="1f050-159">Ubuntu hardware enablement (HWE) kernel:</span></span>

* [<span data-ttu-id="1f050-160">http://blog.utlemming.org/2015/01/ubuntu-1404-Azure-images-Now-Tracking.HTML</span><span class="sxs-lookup"><span data-stu-id="1f050-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span></span>](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [<span data-ttu-id="1f050-161">http://blog.utlemming.org/2015/02/1204-Azure-cloud-images-Now-Using-hwe.HTML</span><span class="sxs-lookup"><span data-stu-id="1f050-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span></span>](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

