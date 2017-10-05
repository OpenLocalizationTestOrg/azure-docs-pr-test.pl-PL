---
title: Przygotowanie Debian dysku VHD systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak utworzyć Debian 7 i 8 pliki VHD dla wdrożenia na platformie Azure."
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
ms.openlocfilehash: 63970d162c12984d6476bf0b9fc4ab70160eccdb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-a-debian-vhd-for-azure"></a><span data-ttu-id="16c85-103">Przygotowywanie wirtualnego dysku twardego systemu Debian dla platformy Azure</span><span class="sxs-lookup"><span data-stu-id="16c85-103">Prepare a Debian VHD for Azure</span></span>
## <a name="prerequisites"></a><span data-ttu-id="16c85-104">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="16c85-104">Prerequisites</span></span>
<span data-ttu-id="16c85-105">W tej sekcji założono zainstalowano system operacyjny Debian Linux z pliku ISO pobrane z [Debian witryny sieci Web](https://www.debian.org/distrib/) do wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="16c85-105">This section assumes that you have already installed a Debian Linux operating system from an .iso file downloaded from the [Debian website](https://www.debian.org/distrib/) to a virtual hard disk.</span></span> <span data-ttu-id="16c85-106">Istnieje wiele narzędzi do tworzenia plików VHD; Funkcja Hyper-V jest tylko przykładem.</span><span class="sxs-lookup"><span data-stu-id="16c85-106">Multiple tools exist to create .vhd files; Hyper-V is only one example.</span></span> <span data-ttu-id="16c85-107">Aby uzyskać instrukcje, za pomocą funkcji Hyper-V, zobacz [Instalowanie roli funkcji Hyper-V i konfigurowanie maszyny wirtualnej](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="16c85-107">For instructions using Hyper-V, see [Install the Hyper-V Role and Configure a Virtual Machine](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

## <a name="installation-notes"></a><span data-ttu-id="16c85-108">Informacje o instalacji</span><span class="sxs-lookup"><span data-stu-id="16c85-108">Installation notes</span></span>
* <span data-ttu-id="16c85-109">Zobacz także [ogólne informacje o instalacji systemu Linux](create-upload-generic.md#general-linux-installation-notes) więcej porad na przygotowanie systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="16c85-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="16c85-110">Nowszy format VHDX nie jest obsługiwane na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="16c85-110">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="16c85-111">Dysk można przekonwertować na format wirtualnego dysku twardego za pomocą Menedżera funkcji Hyper-V lub **convert-vhd** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="16c85-111">You can convert the disk to VHD format using Hyper-V Manager or the **convert-vhd** cmdlet.</span></span>
* <span data-ttu-id="16c85-112">Zalecane jest użycie standardowe partycje, a nie LVM (często domyślnie dla wielu instalacji), podczas instalowania systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="16c85-112">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="16c85-113">Pozwoli to uniknąć konfliktów nazw LVM sklonowany maszyn wirtualnych, szczególnie, jeśli dysk systemu operacyjnego kiedykolwiek musi być dołączony do innej maszyny Wirtualnej do rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="16c85-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="16c85-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) może być używany dla dysków z danymi, jeśli preferowane.</span><span class="sxs-lookup"><span data-stu-id="16c85-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="16c85-115">Nie należy konfigurować wymiany partycji na dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="16c85-115">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="16c85-116">Aby utworzyć plik wymiany na dysku zasobów można skonfigurować agenta systemu Linux platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="16c85-116">The Azure Linux agent can be configured to create a swap file on the temporary resource disk.</span></span> <span data-ttu-id="16c85-117">Więcej informacji na ten temat można znaleźć w poniższych krokach.</span><span class="sxs-lookup"><span data-stu-id="16c85-117">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="16c85-118">Wszystkie wirtualne dyski twarde muszą mieć rozmiary, które są wielokrotności 1 MB.</span><span class="sxs-lookup"><span data-stu-id="16c85-118">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-azure-manage-to-create-debian-vhds"></a><span data-ttu-id="16c85-119">Użyj zarządzania Azure, aby utworzyć wirtualne dyski twarde Debian</span><span class="sxs-lookup"><span data-stu-id="16c85-119">Use Azure-Manage to create Debian VHDs</span></span>
<span data-ttu-id="16c85-120">Brak dostępnych narzędzi do generowania Debian wirtualne dyski twarde dla platformy Azure, takich jak [azure — zarządzanie](https://github.com/credativ/azure-manage) skrypty z [credativ](http://www.credativ.com/).</span><span class="sxs-lookup"><span data-stu-id="16c85-120">There are tools available for generating Debian VHDs for Azure, such as the [azure-manage](https://github.com/credativ/azure-manage) scripts from [credativ](http://www.credativ.com/).</span></span> <span data-ttu-id="16c85-121">Jest to zalecane podejście i tworzenie obrazu od początku.</span><span class="sxs-lookup"><span data-stu-id="16c85-121">This is the recommended approach versus creating an image from scratch.</span></span> <span data-ttu-id="16c85-122">Na przykład, aby utworzyć Debian VHD 8, uruchom następujące polecenia, aby pobrać azure w zarządzaniu (i zależności) i uruchom skrypt azure_build_image:</span><span class="sxs-lookup"><span data-stu-id="16c85-122">For example, to create a Debian 8 VHD run the following commands to download azure-manage (and dependencies) and run the azure_build_image script:</span></span>

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a><span data-ttu-id="16c85-123">Ręcznie przygotowanie Debian wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="16c85-123">Manually prepare a Debian VHD</span></span>
1. <span data-ttu-id="16c85-124">W Menedżerze funkcji Hyper-V wybierz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="16c85-124">In Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="16c85-125">Kliknij przycisk **Connect** aby otworzyć okno konsoli dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="16c85-125">Click **Connect** to open a console window for the virtual machine.</span></span>
3. <span data-ttu-id="16c85-126">Komentarz linii **deb cdrom** w `/etc/apt/source.list` po skonfigurowaniu maszyny Wirtualnej z plikiem ISO.</span><span class="sxs-lookup"><span data-stu-id="16c85-126">Comment out the line for **deb cdrom** in `/etc/apt/source.list` if you set up the VM against an ISO file.</span></span>
4. <span data-ttu-id="16c85-127">Edytuj `/etc/default/grub` plik i zmodyfikuj **GRUB_CMDLINE_LINUX** parametru w następujący sposób, aby uwzględnić jądra dodatkowe parametry dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="16c85-127">Edit the `/etc/default/grub` file and modify the **GRUB_CMDLINE_LINUX** parameter as follows to include additional kernel parameters for Azure.</span></span>
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. <span data-ttu-id="16c85-128">Odbuduj chodników, a następnie uruchom:</span><span class="sxs-lookup"><span data-stu-id="16c85-128">Rebuild the grub and run:</span></span>
   
        # sudo update-grub
6. <span data-ttu-id="16c85-129">Dodaj repozytoria Azure w Debian /etc/apt/sources.list Debian 7 lub 8:</span><span class="sxs-lookup"><span data-stu-id="16c85-129">Add Debian's Azure repositories to /etc/apt/sources.list for either Debian 7 or 8:</span></span>
   
    <span data-ttu-id="16c85-130">**Debian 7.x "Wheezy"**</span><span class="sxs-lookup"><span data-stu-id="16c85-130">**Debian 7.x "Wheezy"**</span></span>
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    <span data-ttu-id="16c85-131">**Debian 8.x "Joasia"**</span><span class="sxs-lookup"><span data-stu-id="16c85-131">**Debian 8.x "Jessie"**</span></span>

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. <span data-ttu-id="16c85-132">Zainstaluj agenta systemu Linux platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="16c85-132">Install the Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. <span data-ttu-id="16c85-133">Debian 7 jest wymagany do uruchamiania na podstawie 3.16 jądra z repozytorium wheezy backports.</span><span class="sxs-lookup"><span data-stu-id="16c85-133">For Debian 7, it is required to run the 3.16-based kernel from the wheezy-backports repository.</span></span> <span data-ttu-id="16c85-134">Najpierw utwórz plik o nazwie /etc/apt/preferences.d/linux.pref z następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="16c85-134">First create a file called /etc/apt/preferences.d/linux.pref with the following contents:</span></span>
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    <span data-ttu-id="16c85-135">Następnie uruchom "sudo instalacji stanie get linux obrazu — amd64" Aby zainstalować nowy jądra.</span><span class="sxs-lookup"><span data-stu-id="16c85-135">Then run "sudo apt-get install linux-image-amd64" to install the new kernel.</span></span>
3. <span data-ttu-id="16c85-136">Anulowanie zastrzeżenia maszyny wirtualnej i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure, a następnie uruchom:</span><span class="sxs-lookup"><span data-stu-id="16c85-136">Deprovision the virtual machine and prepare it for provisioning on Azure and run:</span></span>
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. <span data-ttu-id="16c85-137">Kliknij przycisk **akcji** -> zamykania w dół w Menedżerze funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="16c85-137">Click **Action** -> Shut Down in Hyper-V Manager.</span></span> <span data-ttu-id="16c85-138">Dysk VHD systemu Linux jest teraz gotowy do przekazania do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="16c85-138">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16c85-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="16c85-139">Next steps</span></span>
<span data-ttu-id="16c85-140">Teraz możesz używać Debian wirtualnego dysku twardego do tworzenia nowych maszyn wirtualnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="16c85-140">You're now ready to use your Debian virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="16c85-141">Jeśli jest to czy jest przekazywanie pliku VHD na platformę Azure po raz pierwszy, zobacz kroki 2 i 3 w [tworzenie i przekazywanie wirtualnego dysku twardego, który zawiera system operacyjny Linux](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="16c85-141">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

