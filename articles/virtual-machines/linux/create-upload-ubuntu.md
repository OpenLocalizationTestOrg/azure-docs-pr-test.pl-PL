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
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a>Przygotowywanie maszyny wirtualnej systemu Ubuntu dla platformy Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a>Obrazy Ubuntu oficjalnego w chmurze
Ubuntu teraz publikuje oficjalnego Azure wirtualne dyski twarde do pobrania na [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/). Jeśli konieczne toobuild własne specjalistyczne obrazu Ubuntu na platformie Azure, zamiast hello Procedura ręcznego poniżej jest zalecane toostart z tych znane pracy wirtualne dyski twarde i dostosowywać odpowiednio do potrzeb. najnowsze wersje obraz powitania zawsze można znaleźć pod hello następujących lokalizacji:

* Ubuntu 12.04/dokładne: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)
* Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)
* Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)

## <a name="prerequisites"></a>Wymagania wstępne
W tym artykule przyjęto założenie, zainstalowano wirtualnego dysku twardego Ubuntu Linux systemu operacyjnego tooa. Wiele narzędzi istnieje toocreate plików VHD, na przykład rozwiązanie wirtualizacji takich jak funkcja Hyper-V. Aby uzyskać instrukcje, zobacz [instalowanie hello roli funkcji Hyper-V i konfigurowanie maszyny wirtualnej](http://technet.microsoft.com/library/hh846766.aspx).

**Informacje o instalacji Ubuntu**

* Zobacz także [ogólne informacje o instalacji systemu Linux](create-upload-generic.md#general-linux-installation-notes) więcej porad na przygotowanie systemu Linux na platformie Azure.
* Witaj VHDX format nie jest obsługiwany na platformie Azure, tylko **stały VHD**.  Możesz przekonwertować format tooVHD dysku hello za pomocą Menedżera funkcji Hyper-V lub hello polecenia cmdlet convert-vhd.
* Podczas instalowania systemu Linux hello zaleca się użycie standardowe partycje, a nie LVM (często hello domyślnie wiele instalacji). Pozwoli to uniknąć konfliktów nazw LVM sklonowany maszyn wirtualnych, zwłaszcza w przypadku, gdy na dysku systemu operacyjnego kiedykolwiek wymaga tooanother toobe dołączony maszyny Wirtualnej do rozwiązywania problemów. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) może być używany dla dysków z danymi, jeśli preferowane.
* Nie należy konfigurować partycji wymiany na powitania dysku systemu operacyjnego. agenta systemu Linux Hello może być skonfigurowany toocreate pliku wymiany na powitania zasobów dysku.  Więcej informacji na ten temat można znaleźć w poniższych krokach hello.
* Wszystkie wirtualne dyski twarde hello muszą mieć rozmiary, które są wielokrotności 1 MB.

## <a name="manual-steps"></a>Ręczne
> [!NOTE]
> Przed podjęciem próby wykonania toocreate własny obraz niestandardowy Ubuntu na platformie Azure, należy rozważyć przy użyciu hello wstępnie skompilowany i przetestować obrazy z [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) zamiast tego.
> 
> 

1. W środkowym okienku hello Menedżera funkcji Hyper-V wybierz maszynę wirtualną hello.

2. Kliknij przycisk **Connect** okna hello tooopen hello maszyny wirtualnej.

3. Zastąp bieżący repozytoria hello w Ubuntu hello obrazu toouse repozytoriów Azure. kroki Hello się nieco różnić w zależności od wersji Ubuntu hello.
   
    Przed rozpoczęciem edycji `/etc/apt/sources.list`, jest zalecane toomake kopii zapasowej:
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    Ubuntu 12.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    Ubuntu 14.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    Ubuntu 16.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. Witaj obrazów Ubuntu Azure teraz następujące hello *włączenie sprzętu* jądra (HWE). Aktualizacja hello systemu operacyjnego toohello najnowsze jądra, uruchamiając następujące polecenia hello:

    Ubuntu 12.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    Ubuntu 14.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    Ubuntu 16.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    **Zobacz też:**
    - [https://Wiki.ubuntu.com/Kernel/LTSEnablementStack](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [https://Wiki.ubuntu.com/Kernel/RollingLTSEnablementStack](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. Zmodyfikuj hello jądra rozruchu wiersza chodników tooinclude jądra dodatkowych parametrów dla platformy Azure. toodo tym Otwórz `/etc/default/grub` w edytorze tekstów, Znajdź hello zmiennej o nazwie `GRUB_CMDLINE_LINUX_DEFAULT` (lub Dodaj ją w razie potrzeby) i dokonać jego edycji hello tooinclude następujące parametry:
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    Zapisz i zamknij plik, a następnie uruchom `sudo update-grub`. Daje to pewność, że wszystkie komunikaty konsoli są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy technicznej dotyczącej debugowanie problemów.

6. Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu.  Zazwyczaj jest to domyślna hello.

7. Zainstaluj agenta systemu Linux Azure hello:
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    Witaj `walinuxagent` pakietu może spowodować usunięcie hello `NetworkManager` i `NetworkManager-gnome` pakiety, jeśli są one zainstalowane.

8. Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. Kliknij przycisk **akcji -> zamykania w dół** w Menedżerze funkcji Hyper-V. Dysk VHD systemu Linux jest teraz gotowy toobe przekazać tooAzure.

## <a name="next-steps"></a>Następne kroki
Użytkownik jest teraz gotowy toouse Ubuntu Linux wirtualnego dysku twardego toocreate nowych maszyn wirtualnych na platformie Azure. Jeśli hello jest przesyłana tooAzure pliku VHD powitania po raz pierwszy, zobacz kroki 2 i 3 w [tworzenie i przekazywanie wirtualnego dysku twardego, który zawiera system operacyjny Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="references"></a>Dokumentacja
Ubuntu jądra (HWE) na włączenie sprzętu:

* [http://blog.utlemming.org/2015/01/ubuntu-1404-Azure-images-Now-Tracking.HTML](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [http://blog.utlemming.org/2015/02/1204-Azure-cloud-images-Now-Using-hwe.HTML](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

