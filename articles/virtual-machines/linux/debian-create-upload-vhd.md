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
# <a name="prepare-a-debian-vhd-for-azure"></a>Przygotowywanie wirtualnego dysku twardego systemu Debian dla platformy Azure
## <a name="prerequisites"></a>Wymagania wstępne
W tej sekcji założono zainstalowano system operacyjny Debian Linux z pliku ISO pobrane z hello [Debian witryny sieci Web](https://www.debian.org/distrib/) tooa wirtualnego dysku twardego. Pliki VHD toocreate; istnieje wiele narzędzi Funkcja Hyper-V jest tylko przykładem. Aby uzyskać instrukcje, za pomocą funkcji Hyper-V, zobacz [instalowanie hello roli funkcji Hyper-V i konfigurowanie maszyny wirtualnej](https://technet.microsoft.com/library/hh846766.aspx).

## <a name="installation-notes"></a>Informacje o instalacji
* Zobacz także [ogólne informacje o instalacji systemu Linux](create-upload-generic.md#general-linux-installation-notes) więcej porad na przygotowanie systemu Linux na platformie Azure.
* Witaj nowszy format VHDX nie jest obsługiwane na platformie Azure. Możesz przekonwertować format tooVHD dysku hello za pomocą Menedżera funkcji Hyper-V lub hello **convert-vhd** polecenia cmdlet.
* Podczas instalowania systemu Linux hello zaleca się użycie standardowe partycje, a nie LVM (często hello domyślnie wiele instalacji). Pozwoli to uniknąć konfliktów nazw LVM sklonowany maszyn wirtualnych, zwłaszcza w przypadku, gdy na dysku systemu operacyjnego kiedykolwiek wymaga tooanother toobe dołączony maszyny Wirtualnej do rozwiązywania problemów. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) może być używany dla dysków z danymi, jeśli preferowane.
* Nie należy konfigurować partycji wymiany na powitania dysku systemu operacyjnego. Hello Azure Linux agent może być skonfigurowany toocreate pliku wymiany na powitania zasobów dysku. Więcej informacji na ten temat można znaleźć w poniższych krokach hello.
* Wszystkie wirtualne dyski twarde hello muszą mieć rozmiary, które są wielokrotności 1 MB.

## <a name="use-azure-manage-toocreate-debian-vhds"></a>Użyj zarządzania Azure toocreate Debian wirtualne dyski twarde
Brak dostępnych narzędzi do generowania Debian wirtualne dyski twarde dla platformy Azure, takich jak hello [azure — zarządzanie](https://github.com/credativ/azure-manage) skrypty z [credativ](http://www.credativ.com/). Jest to zalecane podejście i tworzenia obrazu od podstaw hello. Na przykład toocreate Debian 8 VHD uruchom następujące polecenia Zarządzanie azure toodownload hello (i zależności) i uruchom skrypt azure_build_image hello:

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a>Ręcznie przygotowanie Debian wirtualnego dysku twardego
1. W Menedżerze funkcji Hyper-V wybierz hello maszyny wirtualnej.
2. Kliknij przycisk **Connect** tooopen okna konsoli hello maszyny wirtualnej.
3. Komentarz linii hello **deb cdrom** w `/etc/apt/source.list` po skonfigurowaniu hello maszyny Wirtualnej z plikiem ISO.
4. Edytuj hello `/etc/default/grub` plik i zmodyfikuj hello **GRUB_CMDLINE_LINUX** parametru w następujący sposób tooinclude jądra dodatkowe parametry dla platformy Azure.
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. Odbuduj chodników hello, a następnie uruchom:
   
        # sudo update-grub
6. Dodaj too/etc/apt/sources.list repozytoria Azure w Debian Debian 7 lub 8:
   
    **Debian 7.x "Wheezy"**
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    **Debian 8.x "Joasia"**

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. Zainstaluj agenta systemu Linux Azure hello:
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. Debian 7 jest wymagana toorun hello na podstawie 3.16 jądra z repozytorium wheezy backports hello. Najpierw utwórz plik o nazwie /etc/apt/preferences.d/linux.pref z hello następującej zawartości:
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    Następnie uruchom "get stanie sudo zainstalować linux-image-amd64" tooinstall hello nowe jądro.
3. Anulowanie zastrzeżenia hello maszyny wirtualnej i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure, a następnie uruchom:
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. Kliknij przycisk **akcji** -> zamykania w dół w Menedżerze funkcji Hyper-V. Dysk VHD systemu Linux jest teraz gotowy toobe przekazać tooAzure.

## <a name="next-steps"></a>Następne kroki
Użytkownik jest teraz gotowy toouse Debian wirtualnego dysku twardego toocreate nowych maszyn wirtualnych na platformie Azure. Jeśli hello jest przesyłana tooAzure pliku VHD powitania po raz pierwszy, zobacz kroki 2 i 3 w [tworzenie i przekazywanie wirtualnego dysku twardego, który zawiera system operacyjny Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

