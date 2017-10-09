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
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a>Przygotowywanie maszyny wirtualnej systemu SLES lub openSUSE dla platformy Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Wymagania wstępne
W tym artykule przyjęto założenie, że zainstalowano już SUSE lub openSUSE Linux tooa wirtualnego dysku twardego systemu operacyjnego. Wiele narzędzi istnieje toocreate plików VHD, na przykład rozwiązanie wirtualizacji takich jak funkcja Hyper-V. Aby uzyskać instrukcje, zobacz [instalowanie hello roli funkcji Hyper-V i konfigurowanie maszyny wirtualnej](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="sles--opensuse-installation-notes"></a>SLES / openSUSE instalacji uwagi
* Zobacz także [ogólne informacje o instalacji systemu Linux](create-upload-generic.md#general-linux-installation-notes) więcej porad na przygotowanie systemu Linux na platformie Azure.
* Witaj VHDX format nie jest obsługiwany na platformie Azure, tylko **stały VHD**.  Możesz przekonwertować format tooVHD dysku hello za pomocą Menedżera funkcji Hyper-V lub hello polecenia cmdlet convert-vhd.
* Podczas instalowania systemu Linux hello zaleca się użycie standardowe partycje, a nie LVM (często hello domyślnie wiele instalacji). Pozwoli to uniknąć konfliktów nazw LVM sklonowany maszyn wirtualnych, zwłaszcza w przypadku, gdy na dysku systemu operacyjnego kiedykolwiek wymaga tooanother toobe dołączony maszyny Wirtualnej do rozwiązywania problemów. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) może być używany dla dysków z danymi, jeśli preferowane.
* Nie należy konfigurować partycji wymiany na powitania dysku systemu operacyjnego. agenta systemu Linux Hello może być skonfigurowany toocreate pliku wymiany na powitania zasobów dysku.  Więcej informacji na ten temat można znaleźć w poniższych krokach hello.
* Wszystkie wirtualne dyski twarde hello muszą mieć rozmiary, które są wielokrotności 1 MB.

## <a name="use-suse-studio"></a>Użyj SUSE Studio
[SUSE Studio](http://www.susestudio.com) można łatwo tworzyć i zarządzać obrazów SLES i openSUSE platformy Azure i funkcji Hyper-V. Jest to zalecane podejście do dostosowywania własnych obrazów SLES i openSUSE hello.

Jako alternatywne toobuilding własne wirtualnego dysku twardego, SUSE publikuje również obrazów BYOS (Bring Your własnej subskrypcji) dla SLES na [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a>Przygotowanie SUSE Linux Enterprise Server 11 z dodatkiem SP4
1. W środkowym okienku hello Menedżera funkcji Hyper-V wybierz maszynę wirtualną hello.
2. Kliknij przycisk **Connect** okna hello tooopen hello maszyny wirtualnej.
3. Zarejestruj użytkownika tooallow systemu SUSE Linux Enterprise go toodownload aktualizacje i pakiety instalacyjne.
4. Zaktualizuj hello system o najnowszych poprawek hello:
   
        # sudo zypper update
5. Zainstaluj hello agenta systemu Linux platformy Azure z repozytorium SLES hello:
   
        # sudo zypper install WALinuxAgent
6. Sprawdź, czy agenta waagent ustawiono zbyt "on" w chkconfig, a jeśli nie, ją włączyć automatyczne uruchamianie:
   
        # sudo chkconfig waagent on
7. Sprawdź, czy Usługa agenta waagent jest uruchomiona i jeśli nie, uruchom go: 
   
        # sudo service waagent start
8. Zmodyfikuj hello jądra rozruchu liniowego chodników konfiguracji tooinclude jądra dodatkowe parametry dla platformy Azure. toodo tym Otwórz "/ boot/grub/menu.lst" w edytorze tekstów i upewnij się, że hello domyślnego jądra obejmuje hello następujące parametry:
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    Dzięki konsoli komunikaty są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów.
9. Upewnij się, że fstab /boot/grub/menu.lst i/etc/obu dysku hello odwołanie za pomocą jego identyfikatora UUID (przez uuid) zamiast hello identyfikator dysku (według identyfikatora). 
   
    Pobierz identyfikator UUID
   
        # ls /dev/disk/by-uuid/
   
    Jeśli /dev/disk/by-id / jest używany, aktualizacji zarówno /boot/grub/menu.lst i/etc/fstab przy użyciu wartości odpowiednich przez uuid hello
   
    Przed zmianą
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    Po zmianie
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. Zmodyfikuj udev tooavoid zasady generowania statycznych zasady hello interfejsów Ethernet. Te reguły może spowodować problemy podczas klonowania maszyny wirtualnej w Microsoft Azure lub funkcji Hyper-V:
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. Zalecane jest plik hello tooedit "/ etc/sysconfig/sieci/dhcp" i zmień hello `DHCLIENT_SET_HOSTNAME` parametr toohello po:
    
     DHCLIENT_SET_HOSTNAME = "nie"
12. Komentarz "/ etc/sudoers", lub hello następujące wiersze, jeśli istnieją one usunąć:
    
     Ustawienia domyślne targetpw # poprosić o hello hasło użytkownika docelowego hello tj. główny wszystkich ALL=(ALL) wszystkie # ostrzeżenie! Użyj tylko wtedy, wraz z 'Targetpw wartości domyślnych'!
13. Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu.  Zazwyczaj jest to domyślna hello.
14. Nie należy tworzyć obszar wymiany na powitania dysku systemu operacyjnego.
    
    Witaj agenta systemu Linux platformy Azure mogą automatycznie konfigurować obszar wymiany przy użyciu hello zasób lokalny dysk, który jest dołączony toohello maszyny Wirtualnej po zainicjowaniu obsługi administracyjnej na platformie Azure. Ten dysk zasobu lokalnego hello jest *tymczasowego* na dysku i może opróżnić po anulowaną aprowizacją hello maszyny Wirtualnej. Po zainstalowaniu hello Azure agenta systemu Linux (zobacz poprzedni krok) i zmodyfikuj odpowiednio następujące parametry w /etc/waagent.conf hello:
    
     ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Uwaga: Ustaw ten toowhatever muszą toobe.
15. Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:
    
    # <a name="sudo-waagent--force--deprovision"></a>sudo agenta waagent-force - deprovision
    # <a name="export-histsize0"></a>Eksportuj HISTSIZE = 0
    # <a name="logout"></a>Wyloguj
16. Kliknij przycisk **akcji -> zamykania w dół** w Menedżerze funkcji Hyper-V. Dysk VHD systemu Linux jest teraz gotowy toobe przekazać tooAzure.

- - -
## <a name="prepare-opensuse-131"></a>Przygotowanie openSUSE 13.1 +
1. W środkowym okienku hello Menedżera funkcji Hyper-V wybierz maszynę wirtualną hello.
2. Kliknij przycisk **Connect** okna hello tooopen hello maszyny wirtualnej.
3. Na powitania powłoki, uruchom polecenie hello "`zypper lr`". Jeśli to polecenie zwraca dane wyjściowe podobne toohello po, a następnie repozytoria hello są skonfigurowane zgodnie z oczekiwaniami — bez korekt są niezbędne (należy pamiętać, że mogą być różne numery wersji):
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    Jeśli polecenie hello zwraca "Nie zdefiniowano... repozytoria" Użyj hello następujące polecenia tooadd te repozytoriów:
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    Następnie należy sprawdzić repozytoria hello zostały dodane, uruchamiając polecenie hello "`zypper lr`" ponownie. W przypadku, gdy jeden hello repozytoriów odpowiednich aktualizacji nie jest włączona, należy je włączyć, wprowadzając następujące polecenie:
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. Aktualizacja hello jądra toohello najnowszej dostępnej wersji:
   
        # sudo zypper up kernel-default
   
    Lub tooupdate hello systemowi wszystkich najnowszych poprawek hello:
   
        # sudo zypper update
5. Zainstaluj hello agenta systemu Linux platformy Azure.
   
   # <a name="sudo-zypper-install-walinuxagent"></a>Zainstaluj zypper sudo WALinuxAgent
6. Zmodyfikuj hello jądra rozruchu liniowego chodników konfiguracji tooinclude jądra dodatkowe parametry dla platformy Azure. toodo, Otwórz "/ boot/grub/menu.lst" w edytorze tekstów i upewnij się, że hello domyślnego jądra obejmuje hello następujące parametry:
   
     Konsola = ttyS0 earlyprintk = ttyS0 rootdelay = 300
   
   Dzięki konsoli komunikaty są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów. Ponadto należy usunąć hello poniższych parametrów z hello jądra rozruchu wiersza, jeśli istnieją:
   
     Rezerwacja libata.atapi_enabled=0 = 0x1f0, 0x8
7. Zalecane jest plik hello tooedit "/ etc/sysconfig/sieci/dhcp" i zmień hello `DHCLIENT_SET_HOSTNAME` parametr toohello po:
   
     DHCLIENT_SET_HOSTNAME = "nie"
8. **Ważne:** w "/ etc/sudoers", komentarz lub usunąć hello następujące wiersze, jeśli istnieją:
   
     Ustawienia domyślne targetpw # poprosić o hello hasło użytkownika docelowego hello tj. główny wszystkich ALL=(ALL) wszystkie # ostrzeżenie! Użyj tylko wtedy, wraz z 'Targetpw wartości domyślnych'!
9. Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu.  Zazwyczaj jest to domyślna hello.
10. Nie należy tworzyć obszar wymiany na powitania dysku systemu operacyjnego.
    
    Witaj agenta systemu Linux platformy Azure mogą automatycznie konfigurować obszar wymiany przy użyciu hello zasób lokalny dysk, który jest dołączony toohello maszyny Wirtualnej po zainicjowaniu obsługi administracyjnej na platformie Azure. Ten dysk zasobu lokalnego hello jest *tymczasowego* na dysku i może opróżnić po anulowaną aprowizacją hello maszyny Wirtualnej. Po zainstalowaniu hello Azure agenta systemu Linux (zobacz poprzedni krok) i zmodyfikuj odpowiednio następujące parametry w /etc/waagent.conf hello:
    
     ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Uwaga: Ustaw ten toowhatever muszą toobe.
11. Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:
    
    # <a name="sudo-waagent--force--deprovision"></a>sudo agenta waagent-force - deprovision
    # <a name="export-histsize0"></a>Eksportuj HISTSIZE = 0
    # <a name="logout"></a>Wyloguj
12. Upewnij się, powitalne agenta systemu Linux platformy Azure jest uruchamiany podczas uruchamiania:
    
        # sudo systemctl enable waagent.service
13. Kliknij przycisk **akcji -> zamykania w dół** w Menedżerze funkcji Hyper-V. Dysk VHD systemu Linux jest teraz gotowy toobe przekazać tooAzure.

## <a name="next-steps"></a>Następne kroki
Użytkownik jest teraz gotowy toouse SUSE Linux wirtualnego dysku twardego toocreate nowych maszyn wirtualnych na platformie Azure. Jeśli hello jest przesyłana tooAzure pliku VHD powitania po raz pierwszy, zobacz kroki 2 i 3 w [tworzenie i przekazywanie wirtualnego dysku twardego, który zawiera system operacyjny Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

