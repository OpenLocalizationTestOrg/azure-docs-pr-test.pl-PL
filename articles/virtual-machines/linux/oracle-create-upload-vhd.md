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
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a>Przygotowywanie maszyny wirtualnej systemu Linux w środowisku Oracle dla platformy Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Wymagania wstępne
W tym artykule przyjęto założenie, zainstalowano wirtualnego dysku twardego Oracle Linux systemu operacyjnego tooa. Wiele narzędzi istnieje toocreate plików VHD, na przykład rozwiązanie wirtualizacji takich jak funkcja Hyper-V. Aby uzyskać instrukcje, zobacz [instalowanie hello roli funkcji Hyper-V i konfigurowanie maszyny wirtualnej](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="oracle-linux-installation-notes"></a>Oracle Linux instalacji uwagi
* Zobacz także [ogólne informacje o instalacji systemu Linux](create-upload-generic.md#general-linux-installation-notes) więcej porad na przygotowanie systemu Linux na platformie Azure.
* Zgodne jądra Red Hat programu Oracle i ich UEK3 (podzielenie Enterprise jądra) w funkcji Hyper-V i platformy Azure są obsługiwane. Aby uzyskać najlepsze rezultaty należy się tooupdate toohello najnowsze jądra podczas przygotowywania Oracle Linux dysk VHD.
* UEK2 programu Oracle nie jest obsługiwana w funkcji Hyper-V i Azure, ponieważ nie ma hello wymagane sterowniki.
* Witaj VHDX format nie jest obsługiwany na platformie Azure, tylko **stały VHD**.  Możesz przekonwertować format tooVHD dysku hello za pomocą Menedżera funkcji Hyper-V lub hello polecenia cmdlet convert-vhd.
* Podczas instalowania systemu Linux hello zaleca się użycie standardowe partycje, a nie LVM (często hello domyślnie wiele instalacji). Pozwoli to uniknąć konfliktów nazw LVM sklonowany maszyn wirtualnych, zwłaszcza w przypadku, gdy na dysku systemu operacyjnego kiedykolwiek wymaga tooanother toobe dołączony maszyny Wirtualnej do rozwiązywania problemów. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) może być używany dla dysków z danymi, jeśli preferowane.
* NUMA nie jest obsługiwana dla większych rozmiarów maszyn wirtualnych ze względu na błąd tooa w wersji jądra systemu Linux poniżej 2.6.37. Ten problem, przede wszystkim na środowisko za pomocą hello nadrzędnego Red Hat 2.6.32 jądra. Ręczna instalacja agenta systemu Linux Azure hello (agenta waagent) automatycznie spowoduje wyłączenie NUMA w konfiguracji CHODNIKÓW hello hello jądra systemu Linux. Więcej informacji na ten temat można znaleźć w poniższych krokach hello.
* Nie należy konfigurować partycji wymiany na powitania dysku systemu operacyjnego. agenta systemu Linux Hello może być skonfigurowany toocreate pliku wymiany na powitania zasobów dysku.  Więcej informacji na ten temat można znaleźć w poniższych krokach hello.
* Wszystkie wirtualne dyski twarde hello muszą mieć rozmiary, które są wielokrotności 1 MB.
* Upewnij się, że hello `Addons` repozytorium jest włączona. Edytuj plik hello `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) lub `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux) i zmień wiersz hello `enabled=0` za`enabled=1` w obszarze **[ol6_addons]** lub **[ol7_addons]** w tym plik.

## <a name="oracle-linux-64"></a>Oracle Linux 6.4 +
Należy wykonać kroki konfiguracji określone w systemie operacyjnym hello na powitania toorun maszyny wirtualnej na platformie Azure.

1. W środkowym okienku hello Menedżera funkcji Hyper-V wybierz maszynę wirtualną hello.
2. Kliknij przycisk **Connect** okna hello tooopen hello maszyny wirtualnej.
3. Odinstaluj NetworkManager, uruchamiając następujące polecenie hello:
   
        # sudo rpm -e --nodeps NetworkManager
   
    **Uwaga:** Jeśli hello pakiet nie jest już zainstalowany, to polecenie zakończy się niepowodzeniem z komunikatem o błędzie. Taki stan jest oczekiwany.
4. Utwórz plik o nazwie **sieci** w hello `/etc/sysconfig/` katalog, który zawiera hello następującego tekstu:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. Utwórz plik o nazwie **ifcfg eth0** w hello `/etc/sysconfig/network-scripts/` katalog, który zawiera hello następującego tekstu:
   
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
   
        # chkconfig network on
8. Zainstaluj python pyasn1, uruchamiając następujące polecenie hello:
   
        # sudo yum install python-pyasn1
9. Zmodyfikuj hello jądra rozruchu liniowego chodników konfiguracji tooinclude jądra dodatkowe parametry dla platformy Azure. toodo tym Otwórz "/ boot/grub/menu.lst" w edytorze tekstów i upewnij się, że hello domyślnego jądra obejmuje hello następujące parametry:
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   Dzięki konsoli komunikaty są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów. Spowoduje to wyłączenie NUMA powodu usterki tooa jądra zgodne Red Hat programu Oracle.
   
   Oprócz powyższych toohello, zalecane jest zbyt*Usuń* hello następujące parametry:
   
        rhgb quiet crashkernel=auto
   
   Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie toobe dzienniki hello wysyłane toohello portu szeregowego.
   
   Witaj `crashkernel` opcja może być skonfigurowany w razie potrzeby po lewej, ale należy pamiętać, że ten parametr zmniejszy hello ilość dostępnej pamięci w hello wirtualna najmniej 128 MB, które mogą być problemy na powitania mniejsze rozmiary maszyn wirtualnych.
10. Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu.  Zazwyczaj jest to domyślna hello.
11. Zainstaluj hello agenta systemu Linux platformy Azure, uruchamiając następujące polecenie hello. Najnowsza wersja Hello jest 2.0.15.
    
        # sudo yum install WALinuxAgent
    
    Warto zauważyć, że instalowanie pakietu WALinuxAgent hello spowoduje usunięcie hello NetworkManager pakiety NetworkManager gnome jeśli ich nie zostały już usunięte zgodnie z opisem w kroku 2.
12. Nie należy tworzyć obszar wymiany na powitania dysku systemu operacyjnego.
    
    Witaj agenta systemu Linux platformy Azure mogą automatycznie konfigurować obszar wymiany przy użyciu hello zasób lokalny dysk, który jest dołączony toohello maszyny Wirtualnej po zainicjowaniu obsługi administracyjnej na platformie Azure. Ten dysk zasobu lokalnego hello jest *tymczasowego* na dysku i może opróżnić po anulowaną aprowizacją hello maszyny Wirtualnej. Po zainstalowaniu hello Azure agenta systemu Linux (zobacz poprzedni krok) i zmodyfikuj odpowiednio następujące parametry w /etc/waagent.conf hello:
    
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

- - -
## <a name="oracle-linux-70"></a>Oracle Linux 7.0 +
**Zmiany w Oracle Linux 7**

Przygotowywanie maszyny wirtualnej Oracle Linux 7 dla platformy Azure jest bardzo podobne tooOracle Linux 6, jednak istnieje kilka istotnych różnic, warto zauważyć:

* Zarówno hello Red Hat zgodne jądra, jak i programu Oracle UEK3 są obsługiwane na platformie Azure.  Witaj UEK3 jądra jest zalecane.
* Witaj NetworkManager już pakiet powoduje konflikt z agenta systemu Linux Azure hello. Ten pakiet jest instalowany domyślnie i zaleca się, że nie zostanie usunięta.
* GRUB2 teraz jest używany jako hello inicjującego domyślne, więc hello procedury do edycji parametry jądra został zmieniony (patrz poniżej).
* XFS jest teraz hello domyślnego systemu plików. nadal można użyć systemu plików ext4 Hello, w razie potrzeby.

**Kroki konfiguracji**

1. W Menedżerze funkcji Hyper-V wybierz hello maszyny wirtualnej.
2. Kliknij przycisk **Connect** tooopen okna konsoli hello maszyny wirtualnej.
3. Utwórz plik o nazwie **sieci** w hello `/etc/sysconfig/` katalog, który zawiera hello następującego tekstu:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. Utwórz plik o nazwie **ifcfg eth0** w hello `/etc/sysconfig/network-scripts/` katalog, który zawiera hello następującego tekstu:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. Zmodyfikuj udev tooavoid zasady generowania statycznych zasady hello interfejsów Ethernet. Te reguły może spowodować problemy podczas klonowania maszyny wirtualnej w Microsoft Azure lub funkcji Hyper-V:
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. Upewnij się, że Usługa sieciowa hello rozpocznie się podczas rozruchu, uruchamiając następujące polecenie hello:
   
        # sudo chkconfig network on
7. Zainstaluj pakiet języka python pyasn1 hello, uruchamiając następujące polecenie hello:
   
        # sudo yum install python-pyasn1
8. Uruchom następujące polecenie tooclear hello bieżących yum metadanych hello i zainstaluj wszystkie aktualizacje:
   
        # sudo yum clean all
        # sudo yum -y update
9. Zmodyfikuj hello jądra rozruchu liniowego chodników konfiguracji tooinclude jądra dodatkowe parametry dla platformy Azure. toodo tym Otwórz "/ etc/domyślne/chodników" w hello edytora i edytowanie tekstu `GRUB_CMDLINE_LINUX` parametrów, na przykład:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Dzięki konsoli komunikaty są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów. On również wyłącza hello nowe OEL 7 konwencje nazewnictwa dla kart sieciowych. Oprócz powyższych toohello, zalecane jest zbyt*Usuń* hello następujące parametry:
   
       rhgb quiet crashkernel=auto
   
   Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie toobe dzienniki hello wysyłane toohello portu szeregowego.
   
   Witaj `crashkernel` opcja może być skonfigurowany w razie potrzeby po lewej, ale należy pamiętać, że ten parametr zmniejszy hello ilość dostępnej pamięci w hello wirtualna najmniej 128 MB, które mogą być problemy na powitania mniejsze rozmiary maszyn wirtualnych.
10. Po zakończeniu edycji "/ etc/domyślne/chodników" na powyżej, uruchom hello następujące polecenia toorebuild hello chodników konfiguracji:
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu.  Zazwyczaj jest to domyślna hello.
12. Zainstaluj agenta systemu Linux Azure hello, uruchamiając następujące polecenie hello:
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. Nie należy tworzyć obszar wymiany na powitania dysku systemu operacyjnego.
    
    Witaj agenta systemu Linux platformy Azure mogą automatycznie konfigurować obszar wymiany przy użyciu hello zasób lokalny dysk, który jest dołączony toohello maszyny Wirtualnej po zainicjowaniu obsługi administracyjnej na platformie Azure. Ten dysk zasobu lokalnego hello jest *tymczasowego* na dysku i może opróżnić po anulowaną aprowizacją hello maszyny Wirtualnej. Po zainstalowaniu hello Azure agenta systemu Linux (zobacz poprzedni krok hello) i zmodyfikuj odpowiednio następujące parametry w /etc/waagent.conf hello:
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
14. Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. Kliknij przycisk **akcji -> zamykania w dół** w Menedżerze funkcji Hyper-V. Dysk VHD systemu Linux jest teraz gotowy toobe przekazać tooAzure.

## <a name="next-steps"></a>Następne kroki
Użytkownik jest teraz gotowy toouse Oracle Linux VHD toocreate nowych maszyn wirtualnych na platformie Azure. Jeśli hello jest przesyłana tooAzure pliku VHD powitania po raz pierwszy, zobacz kroki 2 i 3 w [tworzenie i przekazywanie wirtualnego dysku twardego, który zawiera system operacyjny Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

