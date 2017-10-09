---
title: "aaaCreate i przekazać Red Hat Enterprise Linux wirtualnego dysku twardego do użycia na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się toocreate i przekaż Azure wirtualnego dysku twardego (VHD) z systemem operacyjnym Red Hat Linux."
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
ms.openlocfilehash: bdd1bbfbee55b5cc61d69a09b06b6bd2c3de362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a>Przygotowywanie maszyny wirtualnej systemu Red Hat dla platformy Azure
W tym artykule przedstawiono sposób tooprepare maszynę wirtualną Red Hat Enterprise Linux (RHEL) do użycia na platformie Azure. Hello wersje RHEL, które zostały omówione w tym artykule są 6.7 + i 7.1 +. Witaj funkcji hypervisor w celu przygotowania, które zostały omówione w tym artykule są maszyny wirtualnej funkcji Hyper-V, na podstawie jądra (KVM) i VMware. Aby uzyskać więcej informacji o wymaganiach dotyczących kwalifikuje się do uczestnictwa w programie dostęp do chmury Red Hat, zobacz [Red Hat dostęp do chmury witryny sieci Web](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) i [systemem RHEL na platformie Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a>Przygotowywanie maszyny wirtualnej z systemem Red Hat z Menedżera funkcji Hyper-V

### <a name="prerequisites"></a>Wymagania wstępne
W tej sekcji założono już uzyskane plik ISO z witryny sieci Web hello Red Hat i zainstalowanych hello RHEL obrazu tooa wirtualnego dysku twardego (VHD). Aby uzyskać więcej informacji o tym, jak toouse Menedżera funkcji Hyper-V tooinstall obrazu systemu operacyjnego, zobacz [instalowanie hello roli funkcji Hyper-V i konfigurowanie maszyny wirtualnej](http://technet.microsoft.com/library/hh846766.aspx).

**RHEL uwagi instalacji**

* Azure nie obsługuje formatu VHDX hello. Azure obsługuje tylko stałe wirtualnego dysku twardego. Można użyć formatu tooVHD dysku hello tooconvert Menedżera funkcji Hyper-V, lub można użyć polecenia cmdlet convert-vhd hello. Jeśli używasz VirtualBox, wybierz **stały rozmiar** nazwą domyślną toohello dynamicznie przydzielane opcji podczas tworzenia dysku hello.
* Azure obsługuje tylko maszyny wirtualne generacji 1. Maszyny wirtualne generacji 1 można przekonwertować z formatu pliku wirtualnego dysku twardego toohello VHDX i dynamicznie powiększający się dysk o stałym rozmiarze tooa. Nie można zmienić generację maszyny wirtualnej. Aby uzyskać więcej informacji, zobacz [należy tworzyć maszyny wirtualne generacji 1 lub 2 w funkcji Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).
* Witaj maksymalny rozmiar, jaki jest dozwolony dla hello wirtualnego dysku twardego jest 1,023 GB.
* Po zainstalowaniu systemu operacyjnego Linux hello firma Microsoft zaleca użycie standardowe partycje, a nie logiczne woluminu Manager (LVM), często jest domyślna powitania dla wielu urządzeń. Takie rozwiązanie pozwoli uniknąć LVM nazwa powoduje konflikt z sklonowane maszyny wirtualne, szczególnie jeśli kiedykolwiek zajdzie tooattach system operacyjny dysku tooanother identycznej maszyny wirtualnej do rozwiązywania problemów. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) może być używany dla dysków z danymi.
* Wymagana jest obsługa jądra służący do instalowania systemów plików uniwersalny Format dysku (UDF). Przy pierwszym uruchomieniu komputera, na platformy Azure, nośnik hello sformatowany funkcji zdefiniowanej przez użytkownika, który jest dołączony toohello gościa przekazuje hello inicjowania obsługi administracyjnej toohello konfiguracji maszyny wirtualnej systemu Linux. Hello agenta systemu Linux platformy Azure musi być możliwe toomount hello UDF pliku system tooread swojej konfiguracji i aprowizowanie maszyny wirtualnej hello.
* Wersje starsze niż 2.6.37 hello jądra systemu Linux nie obsługują dostępu niejednolitego pamięci (NUMA) w ramach funkcji Hyper-V o dużym rozmiarze maszyny wirtualnej. Ten problem wpływa głównie na starszą dystrybucje Użyj powitania od jądra Red Hat 2.6.32 zostało ustalone w 6.6 RHEL (jądra-2.6.32 504). Systemy, systemem jądra niestandardowych, które są starsze niż 2.6.37 lub systemem RHEL jądra, które są starsze niż 2.6.32-504 należy ustawić hello `numa=off` rozruch parametru w wierszu polecenia jądra hello grub.conf. Aby uzyskać więcej informacji, zobacz Red Hat [KB 436883](https://access.redhat.com/solutions/436883).
* Nie należy konfigurować partycji wymiany na powitania dysku systemu operacyjnego. Witaj agenta systemu Linux może być skonfigurowany toocreate pliku wymiany na powitania zasobów dysku.  Więcej informacji na ten temat można znaleźć w hello następujące kroki.
* Wszystkie wirtualne dyski twarde muszą mieć rozmiary, które są wielokrotności 1 MB.

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a>Przygotowanie RHEL 6 maszyny wirtualnej z Menedżera funkcji Hyper-V

1. W Menedżerze funkcji Hyper-V wybierz hello maszyny wirtualnej.

2. Kliknij przycisk **Connect** tooopen okna konsoli hello maszyny wirtualnej.

3. 6 RHEL NetworkManager może zakłócać hello agenta systemu Linux platformy Azure. Odinstalowania tego pakietu, uruchamiając następujące polecenie hello:
   
        # sudo rpm -e --nodeps NetworkManager

4. Utwórz lub Edytuj hello `/etc/sysconfig/network` pliku, a następnie dodaj hello następującego tekstu:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Utwórz lub Edytuj hello `/etc/sysconfig/network-scripts/ifcfg-eth0` pliku, a następnie dodaj hello następującego tekstu:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Przenieś (albo usuń) tooavoid reguły udev hello generowania statycznych zasady hello interfejs typu Ethernet. Te reguły powodować problemy podczas klonowania maszyny wirtualnej w Microsoft Azure lub funkcji Hyper-V:

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. Upewnij się, że Usługa sieciowa hello zostanie uruchomione w czasie rozruchu, uruchamiając następujące polecenie hello:

        # sudo chkconfig network on

8. Zarejestruj Red Hat subskrypcji tooenable hello instalacji pakietów z repozytorium RHEL hello, uruchamiając następujące polecenie hello:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. Pakiet WALinuxAgent Hello, `WALinuxAgent-<version>`, został naciśnięty toohello Red Hat dodatki repozytorium. Włącz hello dodatki repozytorium, uruchamiając następujące polecenie hello:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. Zmodyfikuj hello jądra rozruchu liniowego chodników konfiguracji tooinclude jądra dodatkowe parametry dla platformy Azure. toodo modyfikacji, otwórz `/boot/grub/menu.lst` w edytorze tekstu i upewnij się, że hello domyślnego jądra obejmuje hello następujące parametry:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    To będzie również upewnij się, że wszystkie komunikaty konsoli są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów.
    
    Ponadto zaleca się usunięcie hello następujące parametry:
    
        rhgb quiet crashkernel=auto
    
    Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie toobe dzienniki hello wysyłane toohello portu szeregowego.  Możesz pozostawić hello `crashkernel` opcji skonfigurowanych w razie potrzeby. Należy pamiętać, że ten parametr zmniejsza hello ilość dostępnej pamięci w maszynie wirtualnej hello najmniej 128 MB. Ta konfiguracja może być problemy na mniejsze rozmiary maszyny wirtualnej.

    >[!Important]
    RHEL 6.5 lub starszej należy również ustawić hello `numa=off` parametru jądra. Zobacz Red Hat [KB 436883](https://access.redhat.com/solutions/436883).

11. Upewnij się, powitania serwera bezpiecznej powłoki (SSH) jest zainstalowany i skonfigurowany toostart w czasie rozruchu, która zwykle jest domyślnie hello. Modyfikowanie hello tooinclude /etc/ssh/sshd_config po wierszu:

        ClientAliveInterval 180

12. Zainstaluj agenta systemu Linux Azure hello, uruchamiając następujące polecenie hello:

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    Instalowanie pakietu WALinuxAgent hello usuwa hello NetworkManager i NetworkManager gnome pakietów, jeśli ich nie zostały już usunięte w kroku 3.

13. Nie należy tworzyć obszar wymiany na powitania dysku systemu operacyjnego.

    Hello agenta systemu Linux platformy Azure może automatycznie skonfigurować obszar wymiany przy użyciu hello dysku zasób lokalny, który jest dołączony toohello maszyny wirtualnej po udostępnieniu hello maszyny wirtualnej na platformie Azure. Należy pamiętać, tym hello lokalnych zasobów dysk jest dyskiem tymczasowego i czy mogą być opróżniany podczas hello maszyny wirtualnej jest anulowana. Po zainstalowaniu agenta systemu Linux Azure hello w poprzednim kroku hello zmodyfikować odpowiednio następujące parametry w /etc/waagent.conf hello:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

14. Wyrejestruj hello subskrypcji (w razie potrzeby), uruchamiając następujące polecenie hello:

        # sudo subscription-manager unregister

15. Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. Kliknij przycisk **akcji** > **zamknąć** w Menedżerze funkcji Hyper-V. Dysk VHD systemu Linux jest teraz gotowy toobe przekazać tooAzure.


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a>Przygotowanie RHEL 7 maszyny wirtualnej z Menedżera funkcji Hyper-V

1. W Menedżerze funkcji Hyper-V wybierz hello maszyny wirtualnej.

2. Kliknij przycisk **Connect** tooopen okna konsoli hello maszyny wirtualnej.

3. Utwórz lub Edytuj hello `/etc/sysconfig/network` pliku, a następnie dodaj hello następującego tekstu:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. Utwórz lub Edytuj hello `/etc/sysconfig/network-scripts/ifcfg-eth0` pliku, a następnie dodaj hello następującego tekstu:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. Upewnij się, że Usługa sieciowa hello zostanie uruchomione w czasie rozruchu, uruchamiając następujące polecenie hello:

        # sudo chkconfig network on

6. Zarejestruj Red Hat subskrypcji tooenable hello instalacji pakietów z repozytorium RHEL hello, uruchamiając następujące polecenie hello:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. Zmodyfikuj hello jądra rozruchu liniowego chodników konfiguracji tooinclude jądra dodatkowe parametry dla platformy Azure. toodo modyfikacji, otwórz `/etc/default/grub` w edytorze tekstów i Edycja hello `GRUB_CMDLINE_LINUX` parametru. Na przykład:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   To będzie również upewnij się, że wszystkie komunikaty konsoli są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów. Ta konfiguracja również wyłącza hello nowych systemów RHEL 7 konwencji nazewnictwa, dla kart sieciowych. Ponadto zaleca się usunięcie hello następujące parametry:
   
        rhgb quiet crashkernel=auto
   
    Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie toobe dzienniki hello wysyłane toohello portu szeregowego. Możesz pozostawić hello `crashkernel` opcji skonfigurowanych w razie potrzeby. Należy pamiętać, że ten parametr zmniejsza hello ilość dostępnej pamięci w maszynie wirtualnej hello najmniej 128 MB, mogą być problemy na mniejsze rozmiary maszyny wirtualnej.

8. Po zakończeniu edycji `/etc/default/grub`Uruchom hello następujące polecenia toorebuild hello chodników konfiguracji:

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu, która zwykle jest domyślnie hello. Modyfikowanie `/etc/ssh/sshd_config` hello tooinclude po wierszu:

        ClientAliveInterval 180

10. Pakiet WALinuxAgent Hello, `WALinuxAgent-<version>`, został naciśnięty toohello Red Hat dodatki repozytorium. Włącz hello dodatki repozytorium, uruchamiając następujące polecenie hello:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. Zainstaluj agenta systemu Linux Azure hello, uruchamiając następujące polecenie hello:

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. Nie należy tworzyć obszar wymiany na powitania dysku systemu operacyjnego.

    Hello agenta systemu Linux platformy Azure może automatycznie skonfigurować obszar wymiany przy użyciu hello dysku zasób lokalny, który jest dołączony toohello maszyny wirtualnej po udostępnieniu hello maszyny wirtualnej na platformie Azure. Należy pamiętać, że hello zasób lokalny dysk jest tymczasowe i może opróżnić, gdy maszyna wirtualna hello jest anulowaną aprowizacją. Po zainstalowaniu agenta systemu Linux Azure hello w poprzednim kroku hello zmodyfikować hello następujące parametry w `/etc/waagent.conf` odpowiednio:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. Jeśli chcesz toounregister hello subskrypcji, uruchom hello następujące polecenie:

        # sudo subscription-manager unregister

14. Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. Kliknij przycisk **akcji** > **zamknąć** w Menedżerze funkcji Hyper-V. Dysk VHD systemu Linux jest teraz gotowy toobe przekazać tooAzure.


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a>Przygotowywanie maszyny wirtualnej z systemem Red Hat z KVM
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a>Przygotowanie maszyny wirtualnej RHEL 6 z KVM

1. Pobierz obraz KVM hello 6 RHEL z hello Red Hat witryny sieci Web.

2. Ustaw hasło główne.

    Generowanie zaszyfrowane hasło, a następnie skopiuj dane wyjściowe polecenia hello hello:

        # openssl passwd -1 changeme

    Ustaw hasło główne z guestfish:
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   Zmień hello drugie pole hello głównego użytkownika z "!" toohello zaszyfrowane hasło.

3. Utwórz maszynę wirtualną w KVM hello qcow2 obrazu. Ustaw typ dysku hello zbyt**qcow2**i ustaw model urządzenia interfejsu sieci wirtualnej hello zbyt**virtio**. Następnie uruchom maszynę wirtualną hello i zaloguj się jako katalogu głównego.

4. Utwórz lub Edytuj hello `/etc/sysconfig/network` pliku, a następnie dodaj hello następującego tekstu:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Utwórz lub Edytuj hello `/etc/sysconfig/network-scripts/ifcfg-eth0` pliku, a następnie dodaj hello następującego tekstu:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Przenieś (albo usuń) tooavoid reguły udev hello generowania statycznych zasady hello interfejs typu Ethernet. Te reguły powodować problemy podczas klonowania maszyny wirtualnej Azure lub funkcji Hyper-V:

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. Upewnij się, że Usługa sieciowa hello zostanie uruchomione w czasie rozruchu, uruchamiając następujące polecenie hello:

        # chkconfig network on

8. Zarejestruj Red Hat subskrypcji tooenable hello instalacji pakietów z repozytorium RHEL hello, uruchamiając następujące polecenie hello:

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. Zmodyfikuj hello jądra rozruchu liniowego chodników konfiguracji tooinclude jądra dodatkowe parametry dla platformy Azure. toodo tej konfiguracji, otwórz `/boot/grub/menu.lst` w edytorze tekstu i upewnij się, że hello domyślnego jądra obejmuje hello następujące parametry:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    To będzie również upewnij się, że wszystkie komunikaty konsoli są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów.
    
    Ponadto zaleca się usunięcie hello następujące parametry:
    
        rhgb quiet crashkernel=auto
    
    Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie toobe dzienniki hello wysyłane toohello portu szeregowego. Możesz pozostawić hello `crashkernel` opcji skonfigurowanych w razie potrzeby. Należy pamiętać, że ten parametr zmniejsza hello ilość dostępnej pamięci w maszynie wirtualnej hello najmniej 128 MB, mogą być problemy na mniejsze rozmiary maszyny wirtualnej.

    >[!Important]
    RHEL 6.5 lub starszej należy również ustawić hello `numa=off` parametru jądra. Zobacz Red Hat [KB 436883](https://access.redhat.com/solutions/436883).

10. Dodawanie funkcji Hyper-V tooinitramfs modułów:  

    Edytuj `/etc/dracut.conf`i Dodaj hello następującej zawartości:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Odbuduj initramfs:

        # dracut -f -v

11. Odinstaluj init chmury:

        # yum remove cloud-init

12. Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu:

        # chkconfig sshd on

    Modyfikowanie hello tooinclude /etc/ssh/sshd_config następujące wiersze:

        PasswordAuthentication yes
        ClientAliveInterval 180

13. Pakiet WALinuxAgent Hello, `WALinuxAgent-<version>`, został naciśnięty toohello Red Hat dodatki repozytorium. Włącz hello dodatki repozytorium, uruchamiając następujące polecenie hello:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. Zainstaluj agenta systemu Linux Azure hello, uruchamiając następujące polecenie hello:

        # yum install WALinuxAgent

        # chkconfig waagent on

15. Hello agenta systemu Linux platformy Azure może automatycznie skonfigurować obszar wymiany przy użyciu hello dysku zasób lokalny, który jest dołączony toohello maszyny wirtualnej po udostępnieniu hello maszyny wirtualnej na platformie Azure. Należy pamiętać, że hello zasób lokalny dysk jest tymczasowe i może opróżnić, gdy maszyna wirtualna hello jest anulowaną aprowizacją. Po zainstalowaniu agenta systemu Linux Azure hello w poprzednim kroku hello zmodyfikować hello następujące parametry w **/etc/waagent.conf** odpowiednio:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Wyrejestruj hello subskrypcji (w razie potrzeby), uruchamiając następujące polecenie hello:

        # subscription-manager unregister

17. Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. Zamknij maszynę wirtualną hello w KVM.

19. Konwertowanie formatu wirtualnego dysku twardego toohello hello qcow2 obrazu.

    Najpierw przekonwertować format tooraw obrazu hello:

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    Upewnij się, że rozmiar hello nieprzetworzone hello jest zgodne z 1 MB. W przeciwnym razie zaokrąglij w górę tooalign rozmiar hello z 1 MB:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Konwertuj hello tooa raw dysku stałym rozmiarze wirtualnego dysku twardego:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a>Przygotowanie maszyny wirtualnej RHEL 7 z KVM

1. Pobierz obraz KVM hello RHEL 7 z hello Red Hat witryny sieci Web. Ta procedura wykorzystuje RHEL 7 jako przykład Witaj.

2. Ustaw hasło główne.

    Generowanie zaszyfrowane hasło, a następnie skopiuj dane wyjściowe polecenia hello hello:

        # openssl passwd -1 changeme

    Ustaw hasło główne z guestfish:

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   Zmień hello drugie pole użytkownika głównego z "!" toohello zaszyfrowane hasło.

3. Utwórz maszynę wirtualną w KVM hello qcow2 obrazu. Ustaw typ dysku hello zbyt**qcow2**i ustaw model urządzenia interfejsu sieci wirtualnej hello zbyt**virtio**. Następnie uruchom maszynę wirtualną hello i zaloguj się jako katalogu głównego.

4. Utwórz lub Edytuj hello `/etc/sysconfig/network` pliku, a następnie dodaj hello następującego tekstu:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Utwórz lub Edytuj hello `/etc/sysconfig/network-scripts/ifcfg-eth0` pliku, a następnie dodaj hello następującego tekstu:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. Upewnij się, że Usługa sieciowa hello zostanie uruchomione w czasie rozruchu, uruchamiając następujące polecenie hello:

        # chkconfig network on

7. Zarejestruj Red Hat subskrypcji tooenable instalacji pakietów z repozytorium RHEL hello, uruchamiając następujące polecenie hello:

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. Zmodyfikuj hello jądra rozruchu liniowego chodników konfiguracji tooinclude jądra dodatkowe parametry dla platformy Azure. toodo tej konfiguracji, otwórz `/etc/default/grub` w edytorze tekstów i Edycja hello `GRUB_CMDLINE_LINUX` parametru. Na przykład:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   To polecenie sprawia, że wszystkie komunikaty konsoli są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów. polecenie Hello również wyłącza hello nowych systemów RHEL 7 konwencji nazewnictwa, dla kart sieciowych. Ponadto zaleca się usunięcie hello następujące parametry:
   
        rhgb quiet crashkernel=auto
   
    Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie toobe dzienniki hello wysyłane toohello portu szeregowego. Możesz pozostawić hello `crashkernel` opcji skonfigurowanych w razie potrzeby. Należy pamiętać, że ten parametr zmniejsza hello ilość dostępnej pamięci w maszynie wirtualnej hello najmniej 128 MB, mogą być problemy na mniejsze rozmiary maszyny wirtualnej.

9. Po zakończeniu edycji `/etc/default/grub`Uruchom hello następujące polecenia toorebuild hello chodników konfiguracji:

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. Dodawanie modułów funkcji Hyper-V do initramfs.

    Edytuj `/etc/dracut.conf` i Dodaj zawartość:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Odbuduj initramfs:

        # dracut -f -v

11. Odinstaluj init chmury:

        # yum remove cloud-init

12. Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu:

        # systemctl enable sshd

    Modyfikowanie hello tooinclude /etc/ssh/sshd_config następujące wiersze:

        PasswordAuthentication yes
        ClientAliveInterval 180

13. Pakiet WALinuxAgent Hello, `WALinuxAgent-<version>`, został naciśnięty toohello Red Hat dodatki repozytorium. Włącz hello dodatki repozytorium, uruchamiając następujące polecenie hello:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. Zainstaluj agenta systemu Linux Azure hello, uruchamiając następujące polecenie hello:

        # yum install WALinuxAgent

    Włącz usługę agenta waagent hello:

        # systemctl enable waagent.service

15. Nie należy tworzyć obszar wymiany na powitania dysku systemu operacyjnego.

    Hello agenta systemu Linux platformy Azure może automatycznie skonfigurować obszar wymiany przy użyciu hello dysku zasób lokalny, który jest dołączony toohello maszyny wirtualnej po udostępnieniu hello maszyny wirtualnej na platformie Azure. Należy pamiętać, że hello zasób lokalny dysk jest tymczasowe i może opróżnić, gdy maszyna wirtualna hello jest anulowaną aprowizacją. Po zainstalowaniu agenta systemu Linux Azure hello w poprzednim kroku hello zmodyfikować hello następujące parametry w `/etc/waagent.conf` odpowiednio:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Wyrejestruj hello subskrypcji (w razie potrzeby), uruchamiając następujące polecenie hello:

        # subscription-manager unregister

17. Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. Zamknij maszynę wirtualną hello w KVM.

19. Konwertowanie formatu wirtualnego dysku twardego toohello hello qcow2 obrazu.

    Najpierw przekonwertować format tooraw obrazu hello:

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    Upewnij się, że rozmiar hello nieprzetworzone hello jest zgodne z 1 MB. W przeciwnym razie zaokrąglij w górę tooalign rozmiar hello z 1 MB:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Konwertuj hello tooa raw dysku stałym rozmiarze wirtualnego dysku twardego:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a>Przygotowywanie maszyny wirtualnej z systemem Red Hat z programu VMware
### <a name="prerequisites"></a>Wymagania wstępne
W tej sekcji założono, zainstalowano RHEL maszyny wirtualnej w środowisku programu VMware. Aby uzyskać więcej informacji o tooinstall systemu operacyjnego w programie VMware, zobacz temat [Przewodnik instalacji systemu operacyjnego gościa VMware](http://partnerweb.vmware.com/GOSIG/home.html).

* Po zainstalowaniu systemu operacyjnego Linux hello firma Microsoft zaleca użycie standardowe partycje, a nie LVM, często jest domyślna powitania dla wielu urządzeń. Pozwoli to uniknąć konfliktów nazw LVM ze sklonowanej maszyny wirtualnej, szczególnie w przypadku, jeśli kiedykolwiek dysku systemu operacyjnego musi maszyny wirtualnej tooanother toobe dołączony do rozwiązywania problemów. LVM RAID można lub na dyskach danych, jeśli preferowane.
* Nie należy konfigurować partycji wymiany na powitania dysku systemu operacyjnego. Można skonfigurować hello Linux agent toocreate pliku wymiany na powitania zasobów dysku. Więcej informacji na ten temat można znaleźć w hello kroki, które należy wykonać.
* Podczas tworzenia wirtualnego dysku twardego hello wybrać **magazynu wirtualnego dysku w postaci jednego pliku**.

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a>Przygotowanie RHEL 6 maszyny wirtualnej z programu VMware
1. 6 RHEL NetworkManager może zakłócać hello agenta systemu Linux platformy Azure. Odinstalowania tego pakietu, uruchamiając następujące polecenie hello:
   
        # sudo rpm -e --nodeps NetworkManager

2. Utwórz plik o nazwie **sieci** w hello/etc/sysconfig/katalogu, który zawiera hello następującego tekstu:

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. Utwórz lub Edytuj hello `/etc/sysconfig/network-scripts/ifcfg-eth0` pliku, a następnie dodaj hello następującego tekstu:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. Przenieś (albo usuń) tooavoid reguły udev hello generowania statycznych zasady hello interfejs typu Ethernet. Te reguły powodować problemy podczas klonowania maszyny wirtualnej Azure lub funkcji Hyper-V:

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. Upewnij się, że Usługa sieciowa hello zostanie uruchomione w czasie rozruchu, uruchamiając następujące polecenie hello:

        # sudo chkconfig network on

6. Zarejestruj Red Hat subskrypcji tooenable hello instalacji pakietów z repozytorium RHEL hello, uruchamiając następujące polecenie hello:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. Pakiet WALinuxAgent Hello, `WALinuxAgent-<version>`, został naciśnięty toohello Red Hat dodatki repozytorium. Włącz hello dodatki repozytorium, uruchamiając następujące polecenie hello:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. Zmodyfikuj hello jądra rozruchu liniowego chodników konfiguracji tooinclude jądra dodatkowe parametry dla platformy Azure. toodo, otwórz `/etc/default/grub` w edytorze tekstów i Edycja hello `GRUB_CMDLINE_LINUX` parametru. Na przykład:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   To będzie również upewnij się, że wszystkie komunikaty konsoli są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów. Ponadto zaleca się usunięcie hello następujące parametry:
   
        rhgb quiet crashkernel=auto
   
    Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie toobe dzienniki hello wysyłane toohello portu szeregowego. Możesz pozostawić hello `crashkernel` opcji skonfigurowanych w razie potrzeby. Należy pamiętać, że ten parametr zmniejsza hello ilość dostępnej pamięci w maszynie wirtualnej hello najmniej 128 MB, mogą być problemy na mniejsze rozmiary maszyny wirtualnej.

9. Dodawanie funkcji Hyper-V tooinitramfs modułów:

    Edytuj `/etc/dracut.conf`i Dodaj hello następującej zawartości:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Odbuduj initramfs:

        # dracut -f -v

10. Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu, która zwykle jest domyślnie hello. Modyfikowanie `/etc/ssh/sshd_config` hello tooinclude po wierszu:

    ClientAliveInterval 180

11. Zainstaluj agenta systemu Linux Azure hello, uruchamiając następujące polecenie hello:

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. Nie należy tworzyć obszar wymiany na powitania dysku systemu operacyjnego.

    Hello agenta systemu Linux platformy Azure może automatycznie skonfigurować obszar wymiany przy użyciu hello dysku zasób lokalny, który jest dołączony toohello maszyny wirtualnej po udostępnieniu hello maszyny wirtualnej na platformie Azure. Należy pamiętać, że hello zasób lokalny dysk jest tymczasowe i może opróżnić, gdy maszyna wirtualna hello jest anulowaną aprowizacją. Po zainstalowaniu agenta systemu Linux Azure hello w poprzednim kroku hello zmodyfikować hello następujące parametry w `/etc/waagent.conf` odpowiednio:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. Wyrejestruj hello subskrypcji (w razie potrzeby), uruchamiając następujące polecenie hello:

        # sudo subscription-manager unregister

14. Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. Zamknij maszynę wirtualną hello i konwersji pliku VHD tooa pliku VMDK hello.

    Najpierw przekonwertować format tooraw obrazu hello:

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    Upewnij się, że rozmiar hello nieprzetworzone hello jest zgodne z 1 MB. W przeciwnym razie zaokrąglij w górę tooalign rozmiar hello z 1 MB:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Konwertuj hello tooa raw dysku stałym rozmiarze wirtualnego dysku twardego:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a>Przygotowanie RHEL 7 maszyny wirtualnej z programu VMware
1. Utwórz lub Edytuj hello `/etc/sysconfig/network` pliku, a następnie dodaj hello następującego tekstu:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. Utwórz lub Edytuj hello `/etc/sysconfig/network-scripts/ifcfg-eth0` pliku, a następnie dodaj hello następującego tekstu:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. Upewnij się, że Usługa sieciowa hello zostanie uruchomione w czasie rozruchu, uruchamiając następujące polecenie hello:

        # sudo chkconfig network on

4. Zarejestruj Red Hat subskrypcji tooenable hello instalacji pakietów z repozytorium RHEL hello, uruchamiając następujące polecenie hello:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. Zmodyfikuj hello jądra rozruchu liniowego chodników konfiguracji tooinclude jądra dodatkowe parametry dla platformy Azure. toodo modyfikacji, otwórz `/etc/default/grub` w edytorze tekstów i Edycja hello `GRUB_CMDLINE_LINUX` parametru. Na przykład:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Taka konfiguracja powoduje, że wszystkie komunikaty konsoli są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów. On również wyłącza hello nowych systemów RHEL 7 konwencje nazewnictwa dla kart sieciowych. Ponadto zaleca się usunięcie hello następujące parametry:
   
        rhgb quiet crashkernel=auto
   
    Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie toobe dzienniki hello wysyłane toohello portu szeregowego. Możesz pozostawić hello `crashkernel` opcji skonfigurowanych w razie potrzeby. Należy pamiętać, że ten parametr zmniejsza hello ilość dostępnej pamięci w maszynie wirtualnej hello najmniej 128 MB, mogą być problemy na mniejsze rozmiary maszyny wirtualnej.

6. Po zakończeniu edycji `/etc/default/grub`Uruchom hello następujące polecenia toorebuild hello chodników konfiguracji:

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. Dodaj tooinitramfs modułów funkcji Hyper-V.

    Edytuj `/etc/dracut.conf`, Dodaj zawartość:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Odbuduj initramfs:

        # dracut -f -v

8. Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu. To ustawienie jest zazwyczaj hello domyślnym. Modyfikowanie `/etc/ssh/sshd_config` hello tooinclude po wierszu:

        ClientAliveInterval 180

9. Pakiet WALinuxAgent Hello, `WALinuxAgent-<version>`, został naciśnięty toohello Red Hat dodatki repozytorium. Włącz hello dodatki repozytorium, uruchamiając następujące polecenie hello:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. Zainstaluj agenta systemu Linux Azure hello, uruchamiając następujące polecenie hello:

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. Nie należy tworzyć obszar wymiany na powitania dysku systemu operacyjnego.

    Hello agenta systemu Linux platformy Azure może automatycznie skonfigurować obszar wymiany przy użyciu hello dysku zasób lokalny, który jest dołączony toohello maszyny wirtualnej po udostępnieniu hello maszyny wirtualnej na platformie Azure. Należy pamiętać, że hello zasób lokalny dysk jest tymczasowe i może opróżnić, gdy maszyna wirtualna hello jest anulowaną aprowizacją. Po zainstalowaniu agenta systemu Linux Azure hello w poprzednim kroku hello zmodyfikować hello następujące parametry w `/etc/waagent.conf` odpowiednio:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

12. Jeśli chcesz toounregister hello subskrypcji, uruchom hello następujące polecenie:

        # sudo subscription-manager unregister

13. Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. Zamknij maszynę wirtualną hello i przekonwertować formatu wirtualnego dysku twardego toohello pliku VMDK hello.

    Najpierw przekonwertować format tooraw obrazu hello:

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    Upewnij się, że rozmiar hello nieprzetworzone hello jest zgodne z 1 MB. W przeciwnym razie zaokrąglij w górę tooalign rozmiar hello z 1 MB:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Konwertuj hello tooa raw dysku stałym rozmiarze wirtualnego dysku twardego:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a>Przygotowywanie maszyny wirtualnej z systemem Red Hat z obrazu ISO za pomocą pliku kickstart automatycznie
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a>Przygotowanie RHEL 7 maszyny wirtualnej z pliku kickstart

1.  Utwórz plik kickstart zawierający powitania po zawartości i Zapisz plik hello. Aby uzyskać szczegółowe informacje o instalacji kickstart, zobacz hello [Przewodnik instalacji Kickstart](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run hello Setup Agent on first boot
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

        # Clear hello MBR
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

        # Power down hello machine after install
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

        # Disable hello root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set hello cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build hello grub cfg
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

2. Umieść plik kickstart hello gdzie hello instalacji systemu do niego dostęp.

3. W Menedżerze funkcji Hyper-V Utwórz nową maszynę wirtualną. Na powitania **Podłączanie wirtualnego dysku twardego** wybierz pozycję **Dołącz wirtualny dysk twardy później**oraz pełną hello Kreatora nowej maszyny wirtualnej.

4. Otwórz ustawienia maszyny wirtualnej hello:

    a.  Dołączanie nowej maszyny wirtualnej toohello wirtualnego dysku twardego. Upewnij się, że tooselect **formatu wirtualnego dysku twardego** i **o stałym rozmiarze**.

    b.  Dołącz instalacji hello stacji dysków DVD toohello ISO.

    c.  Ustaw hello tooboot systemu BIOS z dysku CD.

5. Uruchom maszynę wirtualną hello. Po wyświetleniu Przewodnik instalacji hello naciśnij **kartę** opcje rozruchu hello tooconfigure.

6. Wprowadź `inst.ks=<hello location of hello kickstart file>` na końcu hello hello opcje rozruchu, a następnie naciśnij klawisz **Enter**.

7. Poczekaj na powitania toofinish instalacji. Po zakończeniu hello maszyna wirtualna zostanie zamknięta automatycznie. Dysk VHD systemu Linux jest teraz gotowy toobe przekazać tooAzure.

## <a name="known-issues"></a>Znane problemy
### <a name="hello-hyper-v-driver-could-not-be-included-in-hello-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a>Hello sterownik funkcji Hyper-V nie może znajdować się w hello początkowej dysku RAM, korzystając z funkcji hypervisor z systemem innym niż do funkcji Hyper-V

W niektórych przypadkach instalatorów systemu Linux może nie zawierać sterowników hello funkcji Hyper-v hello początkowej dysku RAM (initrd lub initramfs), chyba że Linux wykryje, że jest on uruchomiony w środowisku funkcji Hyper-V.

Podczas korzystania z tooprepare systemu (czyli Virtualbox, Xen itp.) wirtualizacji innego obrazu systemu Linux, może być konieczne tooensure initrd toorebuild, że co najmniej hello hv_vmbus i hv_storvsc jądra moduły są dostępne na powitania początkowej dysku RAM. To znany problem z co najmniej w systemach, które są oparte na powitania nadrzędnego Red Hat dystrybucji.

tooresolve ten problem, Dodaj tooinitramfs modułów funkcji Hyper-V i odbuduj go:

Edytuj `/etc/dracut.conf`i Dodaj hello następującej zawartości:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

Odbuduj initramfs:

        # dracut -f -v

Aby uzyskać więcej informacji, zobacz hello informacji [odbudowywania initramfs](https://access.redhat.com/solutions/1958).

## <a name="next-steps"></a>Następne kroki
Użytkownik jest teraz gotowy toouse Red Hat Enterprise Linux wirtualnego dysku twardego toocreate nowych maszyn wirtualnych na platformie Azure. Jeśli hello jest przesyłana tooAzure pliku VHD powitania po raz pierwszy, zobacz kroki 2 i 3 w [tworzenie i przekazywanie wirtualnego dysku twardego, który zawiera system operacyjny Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

Aby uzyskać więcej informacji na temat funkcji hypervisor hello, które są certyfikowane toorun Red Hat Enterprise Linux, zobacz [hello Red Hat witryny sieci Web](https://access.redhat.com/certified-hypervisors).
