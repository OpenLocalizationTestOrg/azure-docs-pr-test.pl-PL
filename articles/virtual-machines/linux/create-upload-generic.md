---
title: aaaCreate i przekazywanie wirtualnego dysku twardego systemu Linux na platformie Azure
description: "Dowiedz się toocreate i przekaż Azure wirtualnego dysku twardego (VHD) z systemem operacyjnym Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: d351396c-95a0-4092-b7bf-c6aae0bbd112
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 208e15c035edb5520fc29ba8e4e71c42b041864d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="information-for-non-endorsed-distributions"></a>Informacje o nieobsługiwanych dystrybucjach
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Witaj umowy SLA platformy Azure stosuje toovirtual maszynami hello systemu operacyjnego Linux tylko wtedy, gdy jeden z hello [dystrybucje zatwierdzone](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) jest używany. Dystrybucje pomocą wymaganej konfiguracji hello zatwierdzone na wszystkich dystrybucje systemu Linux, znajdujące się w hello Azure są Galeria obrazów.

* [Dystrybucje zatwierdzone na systemie Linux na platformie Azure —](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Obsługa obrazów systemu Linux na platformie Microsoft Azure](https://support.microsoft.com/kb/2941892)

Wszystkie dystrybucje działających na platformie Azure, należy toomeet szereg wymagań wstępnych toohave tooproperly szansy, uruchom na platformie hello.  Ten artykuł zawiera kompleksowe w żadnym wypadku nie zgodnie z każdym dystrybucji jest inny, i jest dość możliwe, że nawet jeśli spełniają wszystkie hello poniższe kryteria należy toosignificantly dostosować Twojej tooensure systemu Linux, który działa poprawnie na platformie hello.

To dlatego zaleca się uruchamiania jednego z naszych [systemu Linux na dystrybucje zatwierdzone Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Jeśli to możliwe. Witaj następujące artykuły poprowadzi Cię przez jak tooprepare hello różnych zatwierdzone dystrybucje systemu Linux, które są obsługiwane na platformie Azure:

* **[Na podstawie centOS dystrybucji](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian systemu Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

Witaj dalszej części tego artykułu koncentruje się na ogólne wskazówki dotyczące uruchamiania dystrybucji systemu Linux na platformie Azure.

## <a name="general-linux-installation-notes"></a>Informacje o instalacji ogólne systemu Linux
* Witaj VHDX format nie jest obsługiwany na platformie Azure, tylko **stały VHD**.  Możesz przekonwertować format tooVHD dysku hello za pomocą Menedżera funkcji Hyper-V lub hello polecenia cmdlet convert-vhd. Jeśli używasz VirtualBox oznacza to, wybierając **stały rozmiar** jako przeciwieństwie domyślne toohello dynamicznie przydzielane podczas tworzenia dysku hello.
* Azure obsługuje tylko maszyny wirtualne generacji 1. Możesz przekonwertować generacji 1 maszynę wirtualną z formatu pliku wirtualnego dysku twardego toohello VHDX i dynamicznie powiększające się tooa stały rozmiar dysku. Ale nie można zmienić generację maszyny wirtualnej. Aby uzyskać więcej informacji, zobacz [należy tworzyć maszyny wirtualne generacji 1 lub 2 w funkcji Hyper-V?](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)
* Witaj maksymalny rozmiar dozwolony dla hello wirtualny dysk twardy jest 1,023 GB.
* Podczas instalowania systemu Linux hello jest *zalecane* używasz standardowe partycje, a nie LVM (często hello domyślnie wiele instalacji). Pozwoli to uniknąć konfliktów nazw LVM sklonowany maszyn wirtualnych, szczególnie w przypadku, gdy dysk systemu operacyjnego musi kiedykolwiek tooanother toobe dołączony identycznych maszyn wirtualnych do rozwiązywania problemów. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) może być używany dla dysków z danymi.
* Wymagana jest obsługa jądra służący do instalowania systemów plików funkcji zdefiniowanej przez użytkownika. Przy pierwszym uruchomieniu komputera na Azure hello konfiguracji inicjowania obsługi administracyjnej jest przekazywany toohello maszyny Wirtualnej systemu Linux za pomocą nośnika sformatowany funkcji zdefiniowanej przez użytkownika, która jest dołączona toohello gościa. agenta systemu Linux Azure Hello musi być możliwe toomount hello UDF pliku system tooread swojej konfiguracji i udostępnić hello maszyny Wirtualnej.
* Wersje jądra systemu Linux poniżej 2.6.37 nie obsługują NUMA w funkcji Hyper-V o dużym rozmiarze maszyny Wirtualnej. Ten problem wpływa głównie na starszą dystrybucji przy użyciu powitania od Red Hat 2.6.32 jądra i ustalono w RHEL 6.6 (jądra-2.6.32 504). Parametr rozruchu hello komputerów z systemami niestandardowych jądra starsze niż 2.6.37 lub systemem RHEL jądra starsze niż 2.6.32-504 należy ustawić `numa=off` na powitania jądra wiersza polecenia w grub.conf. Aby uzyskać więcej informacji, zobacz Red Hat [KB 436883](https://access.redhat.com/solutions/436883).
* Nie należy konfigurować partycji wymiany na powitania dysku systemu operacyjnego. agenta systemu Linux Hello może być skonfigurowany toocreate pliku wymiany na powitania zasobów dysku.  Więcej informacji na ten temat można znaleźć w poniższych krokach hello.
* Wszystkie wirtualne dyski twarde hello muszą mieć rozmiary, które są wielokrotności 1 MB.

### <a name="installing-kernel-modules-without-hyper-v"></a>Instalowanie modułów jądra bez funkcji Hyper-V
Azure działa na funkcji hypervisor obsługującej hello funkcji Hyper-V, więc Linux wymaga zainstalowania niektórych modułów jądra w kolejności toorun na platformie Azure. Jeśli maszynę Wirtualną, która została utworzona poza funkcji Hyper-V, hello instalatorów systemu Linux nie może zawierać hello sterowniki dla funkcji Hyper-V w początkowej ramdisk hello (initrd lub initramfs), chyba że wykryje, że jest uruchomiona w środowisku funkcji Hyper-V. Korzystając z tooprepare systemu (tj. Virtualbox, KVM itp.) wirtualizacji innego obrazu systemu Linux, może być konieczne toorebuild hello initrd tooensure, że co najmniej hello `hv_vmbus` i `hv_storvsc` modułów jądra są dostępne w początkowej ramdisk hello.  To znany problem z co najmniej na systemy oparte na powitania nadrzędnego Red Hat dystrybucji.

mechanizm Hello odbudowywania hello initrd lub initramfs obrazu może się różnić w zależności od hello dystrybucji. Dokumentacja programu dystrybucji lub obsługę hello prawidłowe procedury.  Oto przykład dla jak toorebuild hello initrd przy użyciu hello `mkinitrd` narzędzie:

Najpierw należy utworzyć kopię zapasową istniejącego obrazu initrd hello:

    # cd /boot
    # sudo cp initrd-`uname -r`.img  initrd-`uname -r`.img.bak

Następnie Odbuduj initrd hello z hello `hv_vmbus` i `hv_storvsc` modułów jądra:

    # sudo mkinitrd --preload=hv_storvsc --preload=hv_vmbus -v -f initrd-`uname -r`.img `uname -r`


### <a name="resizing-vhds"></a>Zmiana rozmiaru wirtualnych dysków twardych
Obrazy VHD na platformie Azure muszą mieć too1MB rozmiar wirtualny wyrównane.  Zwykle wirtualne dyski twarde utworzone za pomocą funkcji Hyper-V powinien już być wyrównane poprawnie.  Jeśli hello wirtualnego dysku twardego nie jest wyrównany poprawnie, a następnie może zostać wyświetlony błąd komunikat podobny toohello po podczas próby toocreate *obrazu* z z wirtualnego dysku twardego:

    "hello VHD http://<mystorageaccount>.blob.core.windows.net/vhds/MyLinuxVM.vhd has an unsupported virtual size of 21475270656 bytes. hello size must be a whole number (in MBs).”

tooremedy hello to można zmienić rozmiar maszyny Wirtualnej przy użyciu konsoli Menedżera funkcji Hyper-V hello lub hello [wirtualnego dysku twardego zmiany rozmiaru](http://technet.microsoft.com/library/hh848535.aspx) polecenia cmdlet programu Powershell.  Jeśli nie zostały uruchomione w środowisku systemu Windows, jest zalecane toouse qemu img tooconvert (w razie potrzeby), a następnie i hello zmiany rozmiaru wirtualnego dysku twardego.

> [!NOTE]
> Jest znaną usterką w wersjach qemu img > = 2.2.1, których wynikiem jest nieprawidłowo sformatowany dysk VHD. Witaj problem został rozwiązany w wersji 2.6 QEMU. Zalecane jest toouse qemu-img 2.2.0 lub małe lub too2.6 aktualizacji lub nowszej. Odwołanie: https://bugs.launchpad.net/qemu/+bug/1490611.
> 
> 

1. Zmiana rozmiaru hello wirtualnego dysku twardego bezpośrednio za pomocą narzędzi takich jak `qemu-img` lub `vbox-manage` może spowodować rozruch wirtualnego dysku twardego.  Dlatego zaleca się toofirst hello Konwertuj obraz dysku RAW tooa wirtualnego dysku twardego.  Obraz maszyny Wirtualnej hello już został utworzony jako obraz dysku surowego (domyślnie hello niektórych funkcji hypervisor, takich jak KVM) może pominąć ten krok:
   
       # qemu-img convert -f vpc -O raw MyLinuxVM.vhd MyLinuxVM.raw

2. Oblicz hello wymagany rozmiar hello tooensure obrazu dysku, który hello rozmiar wirtualny jest wyrównany too1MB.  Witaj następującego skryptu powłoki bash może pomóc to.  skrypt Hello używa "`qemu-img info`" toodetermine hello rozmiar wirtualny hello obrazu dysku, a następnie oblicza toohello rozmiar hello dalej 1 MB:
   
       rawdisk="MyLinuxVM.raw"
       vhddisk="MyLinuxVM.vhd"
   
       MB=$((1024*1024))
       size=$(qemu-img info -f raw --output json "$rawdisk" | \
              gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')
   
       rounded_size=$((($size/$MB + 1)*$MB))
       echo "Rounded Size = $rounded_size"

3. Zmiana rozmiaru dysku raw hello przy użyciu $rounded_size zgodnie z hello powyżej skryptu:
   
       # qemu-img resize MyLinuxVM.raw $rounded_size

4. Teraz, przekonwertować hello RAW dysku zapasowego tooa stały rozmiar wirtualnego dysku twardego:
   
       # qemu-img convert -f raw -o subformat=fixed -O vpc MyLinuxVM.raw MyLinuxVM.vhd

   Lub z wersją qemu **2.6 +** obejmują hello `force_size` opcji:

       # qemu-img convert -f raw -o subformat=fixed,force_size -O vpc MyLinuxVM.raw MyLinuxVM.vhd

## <a name="linux-kernel-requirements"></a>Wymagania dotyczące jądra systemu Linux
Witaj sterowniki usługi integracji systemu Linux (LIS) dla funkcji Hyper-V i platformy Azure są tworzone bezpośrednio toohello nadrzędnego Linux jądra. Wiele dystrybucji, które obejmują najnowszej wersji jądra systemu Linux (tj. 3.x) zostały już te sterowniki, które są dostępne lub w inny sposób dostarczyć backported wersje tych sterowników z ich jądra.  Te sterowniki są stale aktualizowane hello jądra nadrzędnego nowe poprawki i funkcje, więc jeśli to możliwe zaleca toorun [zatwierdzone dystrybucji](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) zawierające te poprawki i aktualizacje.

Jeśli używasz wariant wersji Red Hat Enterprise Linux **6.0 6.3**, musisz wykonać tooinstall hello najnowsze sterowniki usług LIS dla funkcji Hyper-V. można znaleźć sterowniki Hello [w tej lokalizacji](http://go.microsoft.com/fwlink/p/?LinkID=254263&clcid=0x409). Począwszy od RHEL **6.4 +** (i ich pochodnych) sterowniki LIS hello już są dołączone jądra hello i dlatego nie pakietów instalacyjnych dodatkowe są potrzebne toorun tych systemów na platformie Azure.

Jeśli wymagana jest niestandardowe jądra, jest zalecane toouse nowszą wersję jądra (tj. **3.8 +**). Dla tych dystrybucji lub dostawców, którzy mają własne jądra wysiłku będzie wymagane tooregularly Poprawka usterki systemu hello LIS sterowniki z hello nadrzędnego jądra tooyour niestandardowych jądra.  Nawet jeśli już używasz stosunkowo najnowszej wersji jądra, zdecydowanie zaleca się, że śledzenie o tookeep dowolnego powyżej poprawek w hello LIS sterowniki i poprawka usterki systemu tych zgodnie z potrzebami. Witaj lokalizację plików źródłowych sterownik LIS hello jest dostępna w hello [MAINTAINERS](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/MAINTAINERS) pliku w drzewie źródła jądra systemu Linux hello:

    F:    arch/x86/include/asm/mshyperv.h
    F:    arch/x86/include/uapi/asm/hyperv.h
    F:    arch/x86/kernel/cpu/mshyperv.c
    F:    drivers/hid/hid-hyperv.c
    F:    drivers/hv/
    F:    drivers/input/serio/hyperv-keyboard.c
    F:    drivers/net/hyperv/
    F:    drivers/scsi/storvsc_drv.c
    F:    drivers/video/fbdev/hyperv_fb.c
    F:    include/linux/hyperv.h
    F:    tools/hv/

W bardzo minimalny braku hello hello następujące poprawki mają znane problemy toocause na platformie Azure i dlatego te muszą być zawarte w hello jądra. Ta lista w żadnym wypadku nie jest kompletną lub zakończenie wszystkich dystrybucji:

* [ata_piix: odroczenie dysków sterowniki toohello funkcji Hyper-V domyślnie](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/ata/ata_piix.c?id=cd006086fa5d91414d8ff9ff2b78fbb593878e3c)
* [storvsc: konto dla pakietów w drodze w ścieżce RESETOWANIA hello](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/scsi/storvsc_drv.c?id=5c1b10ab7f93d24f29b5630286e323d1c5802d5c)
* [storvsc: unikaj użycia WRITE_SAME](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=3e8f4f4065901c8dfc51407e1984495e1748c090)
* [storvsc: Wyłącz zapisu w tej samej macierzy RAID i sterowniki karty hosta wirtualnego](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=54b2b50c20a61b51199bedb6e5d2f8ec2568fb43)
* [storvsc: poprawka wyłuskania wskaźnika o wartości NULL](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=b12bb60d6c350b348a4e1460cd68f97ccae9822e)
* [storvsc: błędy bufora pierścień może spowodować blokowanie operacji We/Wy](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=e86fb5e8ab95f10ec5f2e9430119d5d35020c951)
* [scsi_sysfs: ochronę przed podwójnego wykonywania __scsi_remove_device](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/scsi_sysfs.c?id=be821fd8e62765de43cc4f0e2db363d0e30a7e9b)

## <a name="hello-azure-linux-agent"></a>Hello Azure agenta systemu Linux
Witaj [agenta systemu Linux Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (agenta waagent) jest wymagana tooproperly obsługi administracyjnej maszyny wirtualnej systemu Linux na platformie Azure. Można uzyskać hello najnowszej wersji, pliku problemy lub przesyłania żądań ściągnięcia na powitania [repozytorium GitHub agenta systemu Linux](https://github.com/Azure/WALinuxAgent).

* w ramach licencji Apache 2.0 hello wydaniu Hello agenta systemu Linux. Wiele dystrybucji już Podaj obr. / min lub deb pakietów hello agenta, a więc w niektórych przypadkach to można instalować i aktualizowane przy minimalnym nakładzie pracy.
* Witaj agenta systemu Linux Azure wymaga Python v2.6 +.
* Hello agent wymaga również hello python pyasn1 modułu. Większości dystrybucji zapewniają jako osobny pakiet, który może zostać zainstalowany.
* W niektórych przypadkach hello agenta systemu Linux platformy Azure może nie być zgodna z NetworkManager. Wiele pakietów RPM/Deb hello podał dystrybucje skonfigurować NetworkManager jako pakiet agenta waagent toohello konflikt i w związku z tym odinstaluje NetworkManager po zainstalowaniu pakietu agenta systemu Linux hello.

## <a name="general-linux-system-requirements"></a>Wymagania ogólne systemu Linux

* Zmodyfikuj hello jądra rozruchu liniowego CHODNIKÓW lub GRUB2 hello tooinclude następujące parametry. Dzięki konsoli komunikaty są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów:
  
        console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300
  
    Dzięki konsoli komunikaty są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów.
  
    Oprócz powyższych toohello, zalecane jest zbyt*Usuń* hello następujące parametry, jeśli istnieją:
  
        rhgb quiet crashkernel=auto
  
    Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie toobe dzienniki hello wysyłane toohello portu szeregowego. Witaj `crashkernel` opcja może być skonfigurowany w razie potrzeby po lewej, ale należy pamiętać, że ten parametr zmniejszy hello ilość dostępnej pamięci w hello wirtualna najmniej 128 MB, które mogą być problemy na powitania mniejsze rozmiary maszyn wirtualnych.

* Instalowanie hello Azure agenta systemu Linux
  
    Hello Azure agenta systemu Linux jest wymagany do obsługi obraz systemu Linux na platformie Azure.  Wiele dystrybucji zapewniają hello agenta jako pakiet RPM lub Deb (pakietów hello jest zwykle nazywane "WALinuxAgent" lub "walinuxagent").  Witaj agenta można także zainstalować ręcznie, wykonując kroki hello hello [przewodnik agenta systemu Linux](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

* Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu.  Zazwyczaj jest to domyślna hello.

* Nie należy tworzyć obszar wymiany na powitania dysk systemu operacyjnego
  
    Witaj agenta systemu Linux platformy Azure mogą automatycznie konfigurować obszar wymiany przy użyciu hello zasób lokalny dysk, który jest dołączony toohello maszyny Wirtualnej po zainicjowaniu obsługi administracyjnej na platformie Azure. Ten dysk zasobu lokalnego hello jest *tymczasowego* na dysku i może opróżnić po anulowaną aprowizacją hello maszyny Wirtualnej. Po zainstalowaniu hello Azure agenta systemu Linux (zobacz poprzedni krok) i zmodyfikuj odpowiednio następujące parametry w /etc/waagent.conf hello:
  
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

* Jako ostatni krok Uruchom hello następującej maszyny wirtualnej hello toodeprovision polecenia:
  
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
  
  > [!NOTE]
  > Na Virtualbox może zostać wyświetlony następujący błąd po uruchomieniu hello "agenta waagent-force - deprovision": `[Errno 5] Input/output error`. Ten komunikat o błędzie nie ma znaczenia krytycznego i można zignorować.
  > 
  > 

* Następnie należy tooshut maszynę wirtualną hello a Przekaż hello tooAzure wirtualnego dysku twardego.

