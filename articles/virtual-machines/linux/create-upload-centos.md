---
title: aaaCreate i przekazywanie dysku VHD na podstawie CentOS Linux na platformie Azure
description: "Dowiedz się toocreate i przekaż Azure wirtualnego dysku twardego (VHD) z systemem operacyjnym na podstawie CentOS Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 0e518e92-e981-43f4-b12c-9cba1064c4bb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 78f36be1d36e3d44cb836c912d143f2c9a72aab5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a>Przygotowywanie maszyny wirtualnej systemu CentOS dla platformy Azure
* [Przygotowanie maszyny wirtualnej CentOS 6.x dla platformy Azure](#centos-6x)
* [Przygotowanie maszyny wirtualnej CentOS 7.0 + Azure](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Wymagania wstępne
W tym artykule przyjęto założenie, zainstalowano CentOS (lub podobny pochodnej) Linux tooa wirtualnego dysku twardego systemu operacyjnego. Wiele narzędzi istnieje toocreate plików VHD, na przykład rozwiązanie wirtualizacji takich jak funkcja Hyper-V. Aby uzyskać instrukcje, zobacz [instalowanie hello roli funkcji Hyper-V i konfigurowanie maszyny wirtualnej](http://technet.microsoft.com/library/hh846766.aspx).

**Informacje o instalacji centOS**

* Zobacz także [ogólne informacje o instalacji systemu Linux](create-upload-generic.md#general-linux-installation-notes) więcej porad na przygotowanie systemu Linux na platformie Azure.
* Witaj VHDX format nie jest obsługiwany na platformie Azure, tylko **stały VHD**.  Możesz przekonwertować format tooVHD dysku hello za pomocą Menedżera funkcji Hyper-V lub hello polecenia cmdlet convert-vhd. Jeśli używasz VirtualBox oznacza to, wybierając **stały rozmiar** jako przeciwieństwie domyślne toohello dynamicznie przydzielane podczas tworzenia dysku hello.
* Podczas instalowania systemu Linux hello jest *zalecane* używasz standardowe partycje, a nie LVM (często hello domyślnie wiele instalacji). Pozwoli to uniknąć konfliktów nazw LVM sklonowany maszyn wirtualnych, szczególnie w przypadku, gdy dysk systemu operacyjnego musi kiedykolwiek tooanother toobe dołączony identycznych maszyn wirtualnych do rozwiązywania problemów. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) może być używany dla dysków z danymi.
* Wymagana jest obsługa jądra służący do instalowania systemów plików funkcji zdefiniowanej przez użytkownika. Przy pierwszym uruchomieniu komputera na Azure hello konfiguracji inicjowania obsługi administracyjnej jest przekazywany toohello maszyny Wirtualnej systemu Linux za pomocą nośnika sformatowany funkcji zdefiniowanej przez użytkownika, która jest dołączona toohello gościa. agenta systemu Linux Azure Hello musi być możliwe toomount hello UDF pliku system tooread swojej konfiguracji i udostępnić hello maszyny Wirtualnej.
* Wersje jądra systemu Linux poniżej 2.6.37 nie obsługują NUMA w funkcji Hyper-V o dużym rozmiarze maszyny Wirtualnej. Ten problem wpływa głównie na starszą dystrybucji przy użyciu powitania od Red Hat 2.6.32 jądra i ustalono w RHEL 6.6 (jądra-2.6.32 504). Parametr rozruchu hello komputerów z systemami niestandardowych jądra starsze niż 2.6.37 lub systemem RHEL jądra starsze niż 2.6.32-504 należy ustawić `numa=off` na powitania jądra wiersza polecenia w grub.conf. Aby uzyskać więcej informacji, zobacz Red Hat [KB 436883](https://access.redhat.com/solutions/436883).
* Nie należy konfigurować partycji wymiany na powitania dysku systemu operacyjnego. agenta systemu Linux Hello może być skonfigurowany toocreate pliku wymiany na powitania zasobów dysku.  Więcej informacji na ten temat można znaleźć w poniższych krokach hello.
* Wszystkie wirtualne dyski twarde hello muszą mieć rozmiary, które są wielokrotności 1 MB.

## <a name="centos-6x"></a>CentOS 6.x

1. W Menedżerze funkcji Hyper-V wybierz hello maszyny wirtualnej.

2. Kliknij przycisk **Connect** tooopen okna konsoli hello maszyny wirtualnej.

3. W CentOS 6 NetworkManager może zakłócać hello agenta systemu Linux platformy Azure. Odinstalowania tego pakietu, uruchamiając następujące polecenie hello:
   
        # sudo rpm -e --nodeps NetworkManager

4. Utwórz lub Edytuj plik hello `/etc/sysconfig/network` i Dodaj hello następującego tekstu:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Utwórz lub Edytuj plik hello `/etc/sysconfig/network-scripts/ifcfg-eth0` i Dodaj hello następującego tekstu:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Zmodyfikuj udev tooavoid zasady generowania statycznych zasady hello interfejsów Ethernet. Te reguły może spowodować problemy podczas klonowania maszyny wirtualnej w Microsoft Azure lub funkcji Hyper-V:
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. Upewnij się, że Usługa sieciowa hello rozpocznie się podczas rozruchu, uruchamiając następujące polecenie hello:
   
        # sudo chkconfig network on

8. Jeśli chcesz toouse hello OpenLogic duplikatów, które znajdują się w obrębie hello centrach danych platformy Azure, Zastąp hello `/etc/yum.repos.d/CentOS-Base.repo` pliku z powitania po repozytoriów.  Spowoduje to również dodanie hello **[openlogic]** repozytorium, zawierający dodatkowe pakiety, takie jak agenta systemu Linux Azure hello:

        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #contrib - packages by Centos Users
        [contrib]
        name=CentOS-$releasever - Contrib
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=contrib&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/contrib/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

    >[!Note]
    Witaj dalszej części tego przewodnika zakłada, używane są co najmniej hello `[openlogic]` repozytorium, która będzie agenta systemu Linux Azure hello tooinstall używane poniżej.


9. Dodaj powitania po too/etc/yum.conf wiersza:
    
        http_caching=packages

10. Uruchom następujące polecenie tooclear hello bieżącego yum metadanych i aktualizacji hello systemu z najnowszych pakietów hello hello:
    
        # yum clean all

    Jeśli tworzysz obrazu dla starszej wersji CentOS, zalecane jest tooupdate, który hello wszystkie pakiety toohello najnowsza wersja:

        # sudo yum -y update

    Po uruchomieniu tego polecenia może być wymagane ponowne uruchomienie komputera.

11. (Opcjonalnie) Zainstaluj sterowniki hello hello usługi integracji systemu Linux (LIS).
   
    >[!IMPORTANT]
    krok Hello jest **wymagane** dla CentOS 6.3 i wcześniejszych oraz opcjonalny w przypadku nowszych wersjach.

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    Alternatywnie możesz wykonać instrukcje dotyczące ręcznej instalacji hello na powitania [stronę pobierania LIS](https://go.microsoft.com/fwlink/?linkid=403033) hello tooinstall obr. / min na maszynie Wirtualnej.
 
12. Zainstaluj hello Azure agenta systemu Linux oraz zależności:
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    Pakiet WALinuxAgent Hello spowoduje usunięcie hello NetworkManager i NetworkManager gnome pakietów, jeśli ich nie zostały już usunięte zgodnie z opisem w kroku 3.


13. Zmodyfikuj hello jądra rozruchu liniowego chodników konfiguracji tooinclude jądra dodatkowe parametry dla platformy Azure. toodo, otwórz `/boot/grub/menu.lst` w edytorze tekstów i upewnij się, że hello domyślnego jądra obejmuje hello następujące parametry:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Dzięki konsoli komunikaty są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów.
    
    Oprócz powyższych toohello, zalecane jest zbyt*Usuń* hello następujące parametry:
    
        rhgb quiet crashkernel=auto
    
    Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie toobe dzienniki hello wysyłane toohello portu szeregowego.  Witaj `crashkernel` opcja może być skonfigurowany w razie potrzeby po lewej, ale należy pamiętać, że ten parametr zmniejszy hello ilość dostępnej pamięci w hello wirtualna najmniej 128 MB, które mogą być problemy na powitania mniejsze rozmiary maszyn wirtualnych.

    >[!Important]
    CentOS 6.5 lub starszej należy również ustawić parametr jądra hello `numa=off`. Zobacz Red Hat [KB 436883](https://access.redhat.com/solutions/436883).

14. Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu.  Zazwyczaj jest to domyślna hello.

15. Nie należy tworzyć obszar wymiany na powitania dysku systemu operacyjnego.
    
    Witaj agenta systemu Linux platformy Azure mogą automatycznie konfigurować obszar wymiany przy użyciu hello zasób lokalny dysk, który jest dołączony toohello maszyny Wirtualnej po zainicjowaniu obsługi administracyjnej na platformie Azure. Ten dysk zasobu lokalnego hello jest *tymczasowego* na dysku i może opróżnić po anulowaną aprowizacją hello maszyny Wirtualnej. Po zainstalowaniu hello Azure agenta systemu Linux (zobacz poprzedni krok), zmodyfikuj hello następujące parametry w `/etc/waagent.conf` odpowiednio:
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. Kliknij przycisk **akcji -> zamykania w dół** w Menedżerze funkcji Hyper-V. Dysk VHD systemu Linux jest teraz gotowy toobe przekazać tooAzure.


- - -
## <a name="centos-70"></a>CentOS 7.0 +
**Zmiany w CentOS 7 (lub podobny pochodne)**

Przygotowywanie maszyny wirtualnej CentOS 7 dla platformy Azure jest bardzo podobne tooCentOS 6, jednak istnieje kilka istotnych różnic, warto zauważyć:

* Witaj NetworkManager już pakiet powoduje konflikt z agenta systemu Linux Azure hello. Ten pakiet jest instalowany domyślnie i zaleca się, że nie zostanie usunięta.
* GRUB2 teraz jest używany jako hello inicjującego domyślne, więc hello procedury do edycji parametry jądra został zmieniony (patrz poniżej).
* XFS jest teraz hello domyślnego systemu plików. nadal można użyć systemu plików ext4 Hello, w razie potrzeby.

**Kroki konfiguracji**

1. W Menedżerze funkcji Hyper-V wybierz hello maszyny wirtualnej.

2. Kliknij przycisk **Connect** tooopen okna konsoli hello maszyny wirtualnej.

3. Utwórz lub Edytuj plik hello `/etc/sysconfig/network` i Dodaj hello następującego tekstu:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. Utwórz lub Edytuj plik hello `/etc/sysconfig/network-scripts/ifcfg-eth0` i Dodaj hello następującego tekstu:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. Zmodyfikuj udev tooavoid zasady generowania statycznych zasady hello interfejsów Ethernet. Te reguły może spowodować problemy podczas klonowania maszyny wirtualnej w Microsoft Azure lub funkcji Hyper-V:
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. Jeśli chcesz toouse hello OpenLogic duplikatów, które znajdują się w obrębie hello centrach danych platformy Azure, Zastąp hello `/etc/yum.repos.d/CentOS-Base.repo` pliku z powitania po repozytoriów.  Spowoduje to również dodanie hello **[openlogic]** repozytorium, zawierającą pakietów hello Azure Linux agenta:
   
        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

    >[!Note]
    Witaj dalszej części tego przewodnika zakłada, używane są co najmniej hello `[openlogic]` repozytorium, która będzie agenta systemu Linux Azure hello tooinstall używane poniżej.

7. Uruchom następujące polecenie tooclear hello bieżących yum metadanych hello i zainstaluj wszystkie aktualizacje:
   
        # sudo yum clean all

    Jeśli tworzysz obrazu dla starszej wersji CentOS, zalecane jest tooupdate, który hello wszystkie pakiety toohello najnowsza wersja:

        # sudo yum -y update

    Ponowne uruchomienie, może być wymagane po uruchomieniu tego polecenia.

8. Zmodyfikuj hello jądra rozruchu liniowego chodników konfiguracji tooinclude jądra dodatkowe parametry dla platformy Azure. toodo, otwórz `/etc/default/grub` w hello edytora i edytowanie tekstu `GRUB_CMDLINE_LINUX` parametrów, na przykład:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Dzięki konsoli komunikaty są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów. On również wyłącza hello nowe CentOS 7 konwencje nazewnictwa dla kart sieciowych. Oprócz powyższych toohello, zalecane jest zbyt*Usuń* hello następujące parametry:
   
        rhgb quiet crashkernel=auto
   
    Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie toobe dzienniki hello wysyłane toohello portu szeregowego. Witaj `crashkernel` opcja może być skonfigurowany w razie potrzeby po lewej, ale należy pamiętać, że ten parametr zmniejszy hello ilość dostępnej pamięci w hello wirtualna najmniej 128 MB, które mogą być problemy na powitania mniejsze rozmiary maszyn wirtualnych.

9. Po zakończeniu edycji `/etc/default/grub` na powyżej, uruchom hello następujące polecenia toorebuild hello chodników konfiguracji:
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. Obraz powitania od kompilowania **VMWare, VirtualBox lub KVM:** sterowniki hello funkcji Hyper-V upewnij się, że znajdują się w hello initramfs:
   
   Edytuj `/etc/dracut.conf`, Dodaj zawartość:
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   Odbuduj hello initramfs:
   
        # sudo dracut –f -v

11. Zainstaluj hello Azure agenta systemu Linux oraz zależności:

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. Nie należy tworzyć obszar wymiany na powitania dysku systemu operacyjnego.
   
   Witaj agenta systemu Linux platformy Azure mogą automatycznie konfigurować obszar wymiany przy użyciu hello zasób lokalny dysk, który jest dołączony toohello maszyny Wirtualnej po zainicjowaniu obsługi administracyjnej na platformie Azure. Ten dysk zasobu lokalnego hello jest *tymczasowego* na dysku i może opróżnić po anulowaną aprowizacją hello maszyny Wirtualnej. Po zainstalowaniu hello Azure agenta systemu Linux (zobacz poprzedni krok), zmodyfikuj hello następujące parametry w `/etc/waagent.conf` odpowiednio:
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. Kliknij przycisk **akcji -> zamykania w dół** w Menedżerze funkcji Hyper-V. Dysk VHD systemu Linux jest teraz gotowy toobe przekazać tooAzure.

## <a name="next-steps"></a>Następne kroki
Użytkownik jest teraz gotowy toouse Twojego systemu CentOS Linux wirtualnego dysku twardego toocreate nowych maszyn wirtualnych na platformie Azure. Jeśli hello jest przesyłana tooAzure pliku VHD powitania po raz pierwszy, zobacz kroki 2 i 3 w [tworzenie i przekazywanie wirtualnego dysku twardego, który zawiera system operacyjny Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

