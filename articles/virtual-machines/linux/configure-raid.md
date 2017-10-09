---
title: oprogramowanie aaaConfigure RAID na maszynie wirtualnej z systemem Linux | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak RAID toouse mdadm tooconfigure w systemie Linux na platformie Azure."
services: virtual-machines-linux
documentationcenter: na
author: rickstercdn
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: f3cb2786-bda6-4d2c-9aaf-2db80f490feb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: rclaus
ms.openlocfilehash: f06e2679d953faf88ffee9991226cdb3cc1cbdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-software-raid-on-linux"></a>Konfigurowanie macierzy RAID oprogramowania w systemie Linux
Jest typowe oprogramowania toouse scenariusza RAID na maszynach wirtualnych systemu Linux Azure toopresent wiele danych dołączone dyski jako pojedyncze urządzenie RAID. Zwykle to być wydajności tooimprove używanych i zezwala na lepsze przepustowości w porównaniu toousing jednego dysku.

## <a name="attaching-data-disks"></a>Dołączanie dysków z danymi
Co najmniej dwa dyski danych puste są potrzebne tooconfigure urządzenie RAID.  główną przyczyną Hello tworzenia urządzenia RAID jest tooimprove wydajność We/Wy dysku.  Oparte na potrzeby operacji We/Wy, można wybrać tooattach dysków, które są przechowywane w naszym Standard Storage z zapasowej too500 we/wy/ps na dysku lub naszych magazyn w warstwie Premium z zapasowej too5000 we/wy/ps na dysku. W tym artykule nie przejść do szczegółów na temat tooprovision i dołączyć maszyny wirtualnej systemu Linux tooa dysków danych.  Zobacz artykuł Microsoft Azure hello [podłączyć dysk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) szczegółowe informacje dotyczące sposobu tooattach pustymi danymi dysku tooa maszyny wirtualnej systemu Linux na platformie Azure.

## <a name="install-hello-mdadm-utility"></a>Zainstaluj narzędzie mdadm hello
* **Ubuntu**
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* **CentOS & Oracle Linux**
```bash
sudo yum install mdadm
```

* **SLES i openSUSE**
```bash  
zypper install mdadm
```

## <a name="create-hello-disk-partitions"></a>Tworzenie hello partycji dysku
W tym przykładzie tworzymy partycji jednego dysku na /dev/sdc. Witaj nowej partycji dysku zostanie wywołana /dev/sdc1.

1. Uruchom `fdisk` toobegin tworzenie partycji

    ```bash
    sudo fdisk /dev/sdc
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0xa34cb70c.
    Changes will remain in memory only, until you decide toowrite them.
    After that, of course, hello previous content won't be recoverable.

    WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
                    switch off hello mode (command 'c') and change display units to
                    sectors (command 'u').
    ```

2. Naciśnij przycisk "n" w toocreate monitu hello  **n** wa partycji:

    ```bash
    Command (m for help): n
    ```

3. Następnie naciśnij klawisz "p" toocreate **p**zosta partycji:

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. Naciśnij przycisk '1' tooselect partycji o numerze 1:

    ```bash
    Partition number (1-4): 1
    ```

5. Wybierz hello punkt początkowy hello nowej partycji lub naciśnij klawisz `<enter>` tooaccept hello domyślnej tooplace hello partycji na początku hello hello wolnego miejsca na dysku hello:

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. Wybierz rozmiar hello hello partycji, na przykład typ "+10G" toocreate partycji 10 GB. Możesz również nacisnąć klawisz `<enter>` Utwórz jedną partycję, obejmującej cały dysk hello:

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. Następnie należy zmienić identyfikator hello i **t**ypu hello partycji z domyślnej hello IDENTYFIKATORA "83" tooID (Linux) "fd" (Linux raid automatycznie):

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L toolist codes): fd
    ```

8. Na koniec zapisu hello partycji tabeli toohello dysku i zamknąć fdisk:

    ```bash   
    Command (m for help): w
    hello partition table has been altered!
    ```

## <a name="create-hello-raid-array"></a>Tworzenie hello macierzy RAID
1. powitania po przykładzie zostanie "stripe" (poziom RAID 0) trzy partycji znajdujących się na trzy osobne dyski z danymi (sdc1, sdd1, sde1).  Po wywołaniu metody uruchomi to polecenie nowe urządzenie RAID **/dev/md127** jest tworzony. Należy również zauważyć, że jeśli dane te dyski możemy wcześniej częścią innego unieczynnienia macierzy RAID może być konieczne tooadd hello `--force` toohello parametru `mdadm` polecenia:

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. Utwórz hello system plików na powitania nowe urządzenie RAID
   
    a. **CentOS, Oracle Linux SLES 12, openSUSE i Ubuntu**

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    b. **SLES 11**

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    c. **SLES 11** — umożliwiają boot.md i utworzenie mdadm.conf

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > Po wprowadzeniu zmian w systemie SUSE może być wymagane ponowne uruchomienie komputera. Ten krok jest *nie* wymagane na SLES 12.
   > 
   > 

## <a name="add-hello-new-file-system-tooetcfstab"></a>Dodaj hello nowego pliku systemu zbyt/etc/fstab
> [!IMPORTANT]
> Nieprawidłowo edytowania hello /etc/fstab pliku może spowodować rozruch systemu. Jeśli nie wiesz, zapoznaj się z informacji w sposób tooproperly edytować ten plik dokumentacją toohello dystrybucji. Zalecane jest również, że kopia zapasowa pliku /etc/fstab hello został utworzony przed rozpoczęciem edycji.

1. Utwórz hello żądanego punktu instalacji do nowego systemu plików, na przykład:

    ```bash
    sudo mkdir /data
    ```
2. Podczas edytowania /etc/fstab, hello **UUID** powinny być używane tooreference hello pliku systemu zamiast hello nazwy urządzenia.  Użyj hello `blkid` narzędzie toodetermine hello UUID dla hello nowy system plików:

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. Otwórz /etc/fstab w edytorze tekstów i Dodaj wpis dla hello nowy system plików, na przykład:

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    Lub na **SLES 11**:

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    Następnie zapisz i zamknij /etc/fstab.

4. Testowanie tego etc hello/fstab wpis jest prawidłowy:

    ```bash  
    sudo mount -a
    ```

    Jeśli to polecenie powoduje komunikat o błędzie, sprawdź, czy składnia hello w pliku /etc/fstab hello.
   
    Uruchom hello `mount` systemu plików hello tooensure polecenia:

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. (Opcjonalnie) Parametry przed uszkodzeniami rozruchu
   
    **Konfiguracja fstab**
   
    Wiele dystrybucji obejmują albo hello `nobootwait` lub `nofail` instalacji parametrów, które mogą być dodawane toohello/etc/fstab pliku. Te parametry Zezwalaj na wypadek awarii w przypadku instalowania w określonym systemie plików oraz tooboot toocontinue systemu Linux hello Zezwalaj, nawet jeśli jest system plików tooproperly instalacji hello RAID. Zapoznaj się z dokumentacją tooyour dystrybucji Aby uzyskać więcej informacji na temat tych parametrów.
   
    Przykład (Ubuntu):

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    **Parametry rozruchu systemu Linux**
   
    W dodatku toohello powyżej parametry, hello jądra parametru "`bootdegraded=true`" umożliwiają hello tooboot systemu, nawet jeśli hello RAID jest traktowany jako uszkodzony lub nieprawidłowego działania, na przykład jeśli dysk danych jest przypadkowo usunięty z maszyny wirtualnej hello. Domyślnie to może również spowodować-rozruchowy systemu.
   
    Można znaleźć w dokumentacji tooyour dystrybucji w sposób tooproperly Edytuj parametry jądra. Na przykład w wiele dystrybucji (CentOS, Oracle Linux SLES 11) tych parametrów można dodać ręcznie toohello "`/boot/grub/menu.lst`" pliku.  Na Ubuntu można dodać tego parametru toohello `GRUB_CMDLINE_LINUX_DEFAULT` zmiennej na "/ etc/domyślne/chodników".


## <a name="trimunmap-support"></a>PRZYCINANIE/UNMAP pomocy technicznej
PRZYCINANIE/UNMAP toodiscard operacji obsługi niektóre jądra systemu Linux nieużywanych bloków na dysku hello. Operacje te są szczególnie przydatna w tooinform standardowego magazynu Azure, po usunięciu strony nie są już prawidłowe i mogą zostać odrzucone. Odrzucanie strony można zapisać kosztów, jeśli Tworzenie dużych plików, a następnie usuń je.

> [!NOTE]
> RAID nie mogą wystawiać odrzucenia poleceń, jeśli rozmiar fragmentu hello tablicy hello ustawiono tooless niż domyślne hello (512KB). Jest to spowodowane Usuń mapowanie hello szczegółowości na powitania hosta jest również 512KB. Jeśli zmodyfikowano rozmiar fragmentu hello tablicy za pomocą jego mdadm `--chunk=` parametr, a następnie usuń mapowanie/PRZYCINANIE żądania mogą być ignorowane przez hello jądra.

Istnieją dwa sposoby tooenable PRZYCINANIE obsługi w maszynie Wirtualnej systemu Linux. W zwykły sposób poszukaj dystrybucji hello zalecane podejście:

- Użyj hello `discard` zainstalować opcję `/etc/fstab`, na przykład:

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- W niektórych przypadkach hello `discard` opcji może mieć wpływ na wydajność. Alternatywnie można uruchomić hello `fstrim` ręcznie polecenie z wiersza polecenia hello, lub dodaj je tooyour crontab toorun regularnie:

    **Ubuntu**

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    **RHEL/CentOS**
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
