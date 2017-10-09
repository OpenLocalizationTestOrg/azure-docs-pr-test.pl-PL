---
title: aaaConfigure LVM na maszynie wirtualnej z systemem Linux | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooconfigure LVM w systemie Linux na platformie Azure."
services: virtual-machines-linux
documentationcenter: na
author: szarkos
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: 7f533725-1484-479d-9472-6b3098d0aecc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 8daf792d87c6bb3d91a2eddcd01cfab34fd28cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a>Skonfiguruj LVM na Maszynę wirtualną systemu Linux na platformie Azure
Ten dokument będzie omawiać jak tooconfigure menedżera woluminu logicznego (LVM) w sieci maszyny wirtualnej platformy Azure. Gdy jest możliwe tooconfigure LVM na dowolnym dysku dołączony toohello maszyny wirtualnej, domyślnie większość chmury obrazów nie będą miały LVM skonfigurowane na hello dysku systemu operacyjnego. To jest tooprevent problemy z grup zduplikowanych woluminu, jeśli hello dysk systemu operacyjnego jest kiedykolwiek połączona tooanother wirtualna hello tego samego dystrybucji i typ, np. podczas scenariusza odzyskiwania. Dlatego zalecane jest tylko toouse LVM na powitania dysków z danymi.

## <a name="linear-vs-striped-logical-volumes"></a>Liniowego a woluminy rozłożone logiczne
LVM mogą być używane toocombine liczbę dysków fizycznych w jednym woluminie magazynu. Domyślnie LVM zwykle utworzy liniowej woluminów logicznego, co oznacza, że łączone hello magazynu fizycznego. W takim przypadku operacji odczytu/zapisu będą zwykle wysyłane tylko jednego dysku tooa. Z kolei firma Microsoft można utworzyć woluminy rozłożone logiczne, gdy odczyty i zapisy są dyski rozproszonej toomultiple znajdujących się w grupie woluminu hello (tj. podobne tooRAID0). Ze względu na wydajność prawdopodobnie można toostripe logicznej woluminów tak, że odczyty i zapisy wykorzystanie dysków dołączonych danych.

Ten dokument zostanie opisano, jak toocombine danych kilka dysków w grupie pojedynczy wolumin, a następnie utwórz woluminy rozłożone logiczne. Poniższe kroki Hello są nieco uogólniony toowork z większości dystrybucji. W większości przypadków hello narzędzia i przepływów pracy związanych z zarządzaniem LVM na platformie Azure nie są różni się od innych środowisk. W zwykły sposób również Przejrzyj dostawcą Linux dla dokumentacji i najlepsze rozwiązania dotyczące używania LVM z konkretnym dystrybucji.

## <a name="attaching-data-disks"></a>Dołączanie dysków z danymi
Jeden zazwyczaj będzie toostart z co najmniej dwa dyski pusty danych przy użyciu LVM. Oparte na potrzeby operacji We/Wy, można wybrać tooattach dysków, które są przechowywane w naszym Standard Storage z zapasowej too500 we/wy/ps na dysku lub naszych magazyn w warstwie Premium z zapasowej too5000 we/wy/ps na dysku. W tym artykule nie zostaną umieszczone w szczegółów na temat tooprovision i dołączyć maszyny wirtualnej systemu Linux tooa dysków danych. Zobacz artykuł Microsoft Azure hello [podłączyć dysk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) szczegółowe informacje dotyczące sposobu tooattach pustymi danymi dysku tooa maszyny wirtualnej systemu Linux na platformie Azure.

## <a name="install-hello-lvm-utilities"></a>Zainstaluj narzędzia LVM hello
* **Ubuntu**

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* **RHEL, CentOS i Oracle Linux**

    ```bash   
    sudo yum install lvm2
    ```

* **SLES 12 i openSUSE**

    ```bash   
    sudo zypper install lvm2
    ```

* **SLES 11**

    ```bash   
    sudo zypper install lvm2
    ```

    Na SLES11 trzeba również edytować `/etc/sysconfig/lvm` i ustaw `LVM_ACTIVATED_ON_DISCOVERED` zbyt "Włącz":

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a>Konfigurowanie maszyny wirtualnej z systemem Linux
W tym przewodniku zakładamy, że dołączono trzy dyski danych, których będziemy tooas `/dev/sdc`, `/dev/sdd` i `/dev/sde`. Należy pamiętać, że te nie mogą być zawsze hello tej samej nazwy ścieżki w maszynie Wirtualnej. Można uruchomić "`sudo fdisk -l`" lub podobne polecenie toolist dostępne dyski.

1. Przygotuj woluminy fizyczne hello:

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. Utwórz grupę woluminu. W tym przykładzie wywołania hello woluminu grupy `data-vg01`:

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. Utwórz hello logicznej woluminów. Witaj możemy poniższe polecenie utworzy pojedynczy wolumin logiczną o nazwie `data-lv01` toospan hello cały wolumin grupy, ale należy pamiętać, że jest również możliwe toocreate wiele woluminów logiczne w grupie woluminu hello.

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. Format hello wolumin logiczne

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > Z użyciem SLES11 `-t ext3` zamiast ext4. SLES11 obsługuje tylko systemy plików tooext4 dostęp tylko do odczytu.

## <a name="add-hello-new-file-system-tooetcfstab"></a>Dodaj hello nowego pliku systemu zbyt/etc/fstab
> [!IMPORTANT]
> Nieprawidłowo edycji hello `/etc/fstab` pliku może spowodować rozruch systemu. Jeśli nie wiesz, można znaleźć w dokumentacji toohello dystrybucji Aby uzyskać informacje dotyczące sposobu tooproperly edytować ten plik. Jest również zalecane kopii zapasowej hello `/etc/fstab` plik jest tworzony przed przystąpieniem do edytowania.

1. Utwórz hello żądanego punktu instalacji do nowego systemu plików, na przykład:

    ```bash  
    sudo mkdir /data
    ```

2. Znajdź ścieżki woluminu logicznego hello

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. Otwórz `/etc/fstab` w edytorze tekstów i Dodaj wpis dla hello nowy system plików, na przykład:

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    Następnie zapisz i Zamknij `/etc/fstab`.

4. Testowanie tego hello `/etc/fstab` wpis jest prawidłowy:

    ```bash    
    sudo mount -a
    ```

    Jeśli to polecenie powoduje komunikat o błędzie Sprawdź składnię hello hello `/etc/fstab` pliku.
   
    Uruchom hello `mount` systemu plików hello tooensure polecenia:

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. (Opcjonalnie) Parametry rozruchu przed uszkodzeniami w`/etc/fstab`
   
    Wiele dystrybucji obejmują albo hello `nobootwait` lub `nofail` zainstalować parametrów, które mogą być dodawane toohello `/etc/fstab` pliku. Te parametry Zezwalaj na wypadek awarii w przypadku instalowania w określonym systemie plików oraz tooboot toocontinue systemu Linux hello Zezwalaj, nawet jeśli jest system plików tooproperly instalacji hello RAID. Aby uzyskać więcej informacji na temat tych parametrów, zapoznaj się z dokumentacją tooyour dystrybucji.
   
    Przykład (Ubuntu):

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a>PRZYCINANIE/UNMAP pomocy technicznej
PRZYCINANIE/UNMAP toodiscard operacji obsługi niektóre jądra systemu Linux nieużywanych bloków na dysku hello. Operacje te są szczególnie przydatna w tooinform standardowego magazynu Azure, po usunięciu strony nie są już prawidłowe i mogą zostać odrzucone. Odrzucanie strony można zapisać kosztów, jeśli Tworzenie dużych plików, a następnie usuń je.

Istnieją dwa sposoby tooenable PRZYCINANIE obsługi w maszynie Wirtualnej systemu Linux. W zwykły sposób poszukaj dystrybucji hello zalecane podejście:

- Użyj hello `discard` zainstalować opcję `/etc/fstab`, na przykład:

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- W niektórych przypadkach hello `discard` opcji może mieć wpływ na wydajność. Alternatywnie można uruchomić hello `fstrim` ręcznie polecenie z wiersza polecenia hello, lub dodaj je tooyour crontab toorun regularnie:

    **Ubuntu**

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    **RHEL/CentOS**

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
