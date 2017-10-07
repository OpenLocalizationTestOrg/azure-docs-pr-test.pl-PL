---
title: aaaPrepare Debian dysku VHD w programie Azure systemu Linux | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak pliki toocreate Debian 7 i 8 wirtualnego dysku twardego do wdrożenia na platformie Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: a6de7a7c-cc70-44e7-aed0-2ae6884d401a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: e67d126de3db146357a6509aedb5f478576768f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-debian-vhd-for-azure"></a><span data-ttu-id="6f9c0-103">Przygotowywanie wirtualnego dysku twardego systemu Debian dla platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6f9c0-103">Prepare a Debian VHD for Azure</span></span>
## <a name="prerequisites"></a><span data-ttu-id="6f9c0-104">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6f9c0-104">Prerequisites</span></span>
<span data-ttu-id="6f9c0-105">W tej sekcji założono zainstalowano system operacyjny Debian Linux z pliku ISO pobrane z hello [Debian witryny sieci Web](https://www.debian.org/distrib/) tooa wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="6f9c0-105">This section assumes that you have already installed a Debian Linux operating system from an .iso file downloaded from hello [Debian website](https://www.debian.org/distrib/) tooa virtual hard disk.</span></span> <span data-ttu-id="6f9c0-106">Pliki VHD toocreate; istnieje wiele narzędzi Funkcja Hyper-V jest tylko przykładem.</span><span class="sxs-lookup"><span data-stu-id="6f9c0-106">Multiple tools exist toocreate .vhd files; Hyper-V is only one example.</span></span> <span data-ttu-id="6f9c0-107">Aby uzyskać instrukcje, za pomocą funkcji Hyper-V, zobacz [instalowanie hello roli funkcji Hyper-V i konfigurowanie maszyny wirtualnej](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="6f9c0-107">For instructions using Hyper-V, see [Install hello Hyper-V Role and Configure a Virtual Machine](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

## <a name="installation-notes"></a><span data-ttu-id="6f9c0-108">Informacje o instalacji</span><span class="sxs-lookup"><span data-stu-id="6f9c0-108">Installation notes</span></span>
* <span data-ttu-id="6f9c0-109">Zobacz także [ogólne informacje o instalacji systemu Linux](create-upload-generic.md#general-linux-installation-notes) więcej porad na przygotowanie systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6f9c0-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="6f9c0-110">Witaj nowszy format VHDX nie jest obsługiwane na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6f9c0-110">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="6f9c0-111">Możesz przekonwertować format tooVHD dysku hello za pomocą Menedżera funkcji Hyper-V lub hello **convert-vhd** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6f9c0-111">You can convert hello disk tooVHD format using Hyper-V Manager or hello **convert-vhd** cmdlet.</span></span>
* <span data-ttu-id="6f9c0-112">Podczas instalowania systemu Linux hello zaleca się użycie standardowe partycje, a nie LVM (często hello domyślnie wiele instalacji).</span><span class="sxs-lookup"><span data-stu-id="6f9c0-112">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="6f9c0-113">Pozwoli to uniknąć konfliktów nazw LVM sklonowany maszyn wirtualnych, zwłaszcza w przypadku, gdy na dysku systemu operacyjnego kiedykolwiek wymaga tooanother toobe dołączony maszyny Wirtualnej do rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="6f9c0-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="6f9c0-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) może być używany dla dysków z danymi, jeśli preferowane.</span><span class="sxs-lookup"><span data-stu-id="6f9c0-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="6f9c0-115">Nie należy konfigurować partycji wymiany na powitania dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="6f9c0-115">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="6f9c0-116">Hello Azure Linux agent może być skonfigurowany toocreate pliku wymiany na powitania zasobów dysku.</span><span class="sxs-lookup"><span data-stu-id="6f9c0-116">hello Azure Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span> <span data-ttu-id="6f9c0-117">Więcej informacji na ten temat można znaleźć w poniższych krokach hello.</span><span class="sxs-lookup"><span data-stu-id="6f9c0-117">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="6f9c0-118">Wszystkie wirtualne dyski twarde hello muszą mieć rozmiary, które są wielokrotności 1 MB.</span><span class="sxs-lookup"><span data-stu-id="6f9c0-118">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-azure-manage-toocreate-debian-vhds"></a><span data-ttu-id="6f9c0-119">Użyj zarządzania Azure toocreate Debian wirtualne dyski twarde</span><span class="sxs-lookup"><span data-stu-id="6f9c0-119">Use Azure-Manage toocreate Debian VHDs</span></span>
<span data-ttu-id="6f9c0-120">Brak dostępnych narzędzi do generowania Debian wirtualne dyski twarde dla platformy Azure, takich jak hello [azure — zarządzanie](https://github.com/credativ/azure-manage) skrypty z [credativ](http://www.credativ.com/).</span><span class="sxs-lookup"><span data-stu-id="6f9c0-120">There are tools available for generating Debian VHDs for Azure, such as hello [azure-manage](https://github.com/credativ/azure-manage) scripts from [credativ](http://www.credativ.com/).</span></span> <span data-ttu-id="6f9c0-121">Jest to zalecane podejście i tworzenia obrazu od podstaw hello.</span><span class="sxs-lookup"><span data-stu-id="6f9c0-121">This is hello recommended approach versus creating an image from scratch.</span></span> <span data-ttu-id="6f9c0-122">Na przykład toocreate Debian 8 VHD uruchom następujące polecenia Zarządzanie azure toodownload hello (i zależności) i uruchom skrypt azure_build_image hello:</span><span class="sxs-lookup"><span data-stu-id="6f9c0-122">For example, toocreate a Debian 8 VHD run hello following commands toodownload azure-manage (and dependencies) and run hello azure_build_image script:</span></span>

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a><span data-ttu-id="6f9c0-123">Ręcznie przygotowanie Debian wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="6f9c0-123">Manually prepare a Debian VHD</span></span>
1. <span data-ttu-id="6f9c0-124">W Menedżerze funkcji Hyper-V wybierz hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6f9c0-124">In Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="6f9c0-125">Kliknij przycisk **Connect** tooopen okna konsoli hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6f9c0-125">Click **Connect** tooopen a console window for hello virtual machine.</span></span>
3. <span data-ttu-id="6f9c0-126">Komentarz linii hello **deb cdrom** w `/etc/apt/source.list` po skonfigurowaniu hello maszyny Wirtualnej z plikiem ISO.</span><span class="sxs-lookup"><span data-stu-id="6f9c0-126">Comment out hello line for **deb cdrom** in `/etc/apt/source.list` if you set up hello VM against an ISO file.</span></span>
4. <span data-ttu-id="6f9c0-127">Edytuj hello `/etc/default/grub` plik i zmodyfikuj hello **GRUB_CMDLINE_LINUX** parametru w następujący sposób tooinclude jądra dodatkowe parametry dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6f9c0-127">Edit hello `/etc/default/grub` file and modify hello **GRUB_CMDLINE_LINUX** parameter as follows tooinclude additional kernel parameters for Azure.</span></span>
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. <span data-ttu-id="6f9c0-128">Odbuduj chodników hello, a następnie uruchom:</span><span class="sxs-lookup"><span data-stu-id="6f9c0-128">Rebuild hello grub and run:</span></span>
   
        # sudo update-grub
6. <span data-ttu-id="6f9c0-129">Dodaj too/etc/apt/sources.list repozytoria Azure w Debian Debian 7 lub 8:</span><span class="sxs-lookup"><span data-stu-id="6f9c0-129">Add Debian's Azure repositories too/etc/apt/sources.list for either Debian 7 or 8:</span></span>
   
    <span data-ttu-id="6f9c0-130">**Debian 7.x "Wheezy"**</span><span class="sxs-lookup"><span data-stu-id="6f9c0-130">**Debian 7.x "Wheezy"**</span></span>
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    <span data-ttu-id="6f9c0-131">**Debian 8.x "Joasia"**</span><span class="sxs-lookup"><span data-stu-id="6f9c0-131">**Debian 8.x "Jessie"**</span></span>

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. <span data-ttu-id="6f9c0-132">Zainstaluj agenta systemu Linux Azure hello:</span><span class="sxs-lookup"><span data-stu-id="6f9c0-132">Install hello Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. <span data-ttu-id="6f9c0-133">Debian 7 jest wymagana toorun hello na podstawie 3.16 jądra z repozytorium wheezy backports hello.</span><span class="sxs-lookup"><span data-stu-id="6f9c0-133">For Debian 7, it is required toorun hello 3.16-based kernel from hello wheezy-backports repository.</span></span> <span data-ttu-id="6f9c0-134">Najpierw utwórz plik o nazwie /etc/apt/preferences.d/linux.pref z hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="6f9c0-134">First create a file called /etc/apt/preferences.d/linux.pref with hello following contents:</span></span>
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    <span data-ttu-id="6f9c0-135">Następnie uruchom "get stanie sudo zainstalować linux-image-amd64" tooinstall hello nowe jądro.</span><span class="sxs-lookup"><span data-stu-id="6f9c0-135">Then run "sudo apt-get install linux-image-amd64" tooinstall hello new kernel.</span></span>
3. <span data-ttu-id="6f9c0-136">Anulowanie zastrzeżenia hello maszyny wirtualnej i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure, a następnie uruchom:</span><span class="sxs-lookup"><span data-stu-id="6f9c0-136">Deprovision hello virtual machine and prepare it for provisioning on Azure and run:</span></span>
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. <span data-ttu-id="6f9c0-137">Kliknij przycisk **akcji** -> zamykania w dół w Menedżerze funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="6f9c0-137">Click **Action** -> Shut Down in Hyper-V Manager.</span></span> <span data-ttu-id="6f9c0-138">Dysk VHD systemu Linux jest teraz gotowy toobe przekazać tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6f9c0-138">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f9c0-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6f9c0-139">Next steps</span></span>
<span data-ttu-id="6f9c0-140">Użytkownik jest teraz gotowy toouse Debian wirtualnego dysku twardego toocreate nowych maszyn wirtualnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6f9c0-140">You're now ready toouse your Debian virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="6f9c0-141">Jeśli hello jest przesyłana tooAzure pliku VHD powitania po raz pierwszy, zobacz kroki 2 i 3 w [tworzenie i przekazywanie wirtualnego dysku twardego, który zawiera system operacyjny Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6f9c0-141">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

