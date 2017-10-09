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
# <a name="configure-software-raid-on-linux"></a><span data-ttu-id="785e9-103">Konfigurowanie macierzy RAID oprogramowania w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="785e9-103">Configure Software RAID on Linux</span></span>
<span data-ttu-id="785e9-104">Jest typowe oprogramowania toouse scenariusza RAID na maszynach wirtualnych systemu Linux Azure toopresent wiele danych dołączone dyski jako pojedyncze urządzenie RAID.</span><span class="sxs-lookup"><span data-stu-id="785e9-104">It's a common scenario toouse software RAID on Linux virtual machines in Azure toopresent multiple attached data disks as a single RAID device.</span></span> <span data-ttu-id="785e9-105">Zwykle to być wydajności tooimprove używanych i zezwala na lepsze przepustowości w porównaniu toousing jednego dysku.</span><span class="sxs-lookup"><span data-stu-id="785e9-105">Typically this can be used tooimprove performance and allow for improved throughput compared toousing just a single disk.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="785e9-106">Dołączanie dysków z danymi</span><span class="sxs-lookup"><span data-stu-id="785e9-106">Attaching data disks</span></span>
<span data-ttu-id="785e9-107">Co najmniej dwa dyski danych puste są potrzebne tooconfigure urządzenie RAID.</span><span class="sxs-lookup"><span data-stu-id="785e9-107">Two or more empty data disks are needed tooconfigure a RAID device.</span></span>  <span data-ttu-id="785e9-108">główną przyczyną Hello tworzenia urządzenia RAID jest tooimprove wydajność We/Wy dysku.</span><span class="sxs-lookup"><span data-stu-id="785e9-108">hello primary reason for creating a RAID device is tooimprove performance of your disk IO.</span></span>  <span data-ttu-id="785e9-109">Oparte na potrzeby operacji We/Wy, można wybrać tooattach dysków, które są przechowywane w naszym Standard Storage z zapasowej too500 we/wy/ps na dysku lub naszych magazyn w warstwie Premium z zapasowej too5000 we/wy/ps na dysku.</span><span class="sxs-lookup"><span data-stu-id="785e9-109">Based on your IO needs, you can choose tooattach disks that are stored in our Standard Storage, with up too500 IO/ps per disk or our Premium storage with up too5000 IO/ps per disk.</span></span> <span data-ttu-id="785e9-110">W tym artykule nie przejść do szczegółów na temat tooprovision i dołączyć maszyny wirtualnej systemu Linux tooa dysków danych.</span><span class="sxs-lookup"><span data-stu-id="785e9-110">This article does not go into detail on how tooprovision and attach data disks tooa Linux virtual machine.</span></span>  <span data-ttu-id="785e9-111">Zobacz artykuł Microsoft Azure hello [podłączyć dysk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) szczegółowe informacje dotyczące sposobu tooattach pustymi danymi dysku tooa maszyny wirtualnej systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="785e9-111">See hello Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how tooattach an empty data disk tooa Linux virtual machine on Azure.</span></span>

## <a name="install-hello-mdadm-utility"></a><span data-ttu-id="785e9-112">Zainstaluj narzędzie mdadm hello</span><span class="sxs-lookup"><span data-stu-id="785e9-112">Install hello mdadm utility</span></span>
* <span data-ttu-id="785e9-113">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="785e9-113">**Ubuntu**</span></span>
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* <span data-ttu-id="785e9-114">**CentOS & Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="785e9-114">**CentOS & Oracle Linux**</span></span>
```bash
sudo yum install mdadm
```

* <span data-ttu-id="785e9-115">**SLES i openSUSE**</span><span class="sxs-lookup"><span data-stu-id="785e9-115">**SLES and openSUSE**</span></span>
```bash  
zypper install mdadm
```

## <a name="create-hello-disk-partitions"></a><span data-ttu-id="785e9-116">Tworzenie hello partycji dysku</span><span class="sxs-lookup"><span data-stu-id="785e9-116">Create hello disk partitions</span></span>
<span data-ttu-id="785e9-117">W tym przykładzie tworzymy partycji jednego dysku na /dev/sdc.</span><span class="sxs-lookup"><span data-stu-id="785e9-117">In this example, we create a single disk partition on /dev/sdc.</span></span> <span data-ttu-id="785e9-118">Witaj nowej partycji dysku zostanie wywołana /dev/sdc1.</span><span class="sxs-lookup"><span data-stu-id="785e9-118">hello new disk partition will be called /dev/sdc1.</span></span>

1. <span data-ttu-id="785e9-119">Uruchom `fdisk` toobegin tworzenie partycji</span><span class="sxs-lookup"><span data-stu-id="785e9-119">Start `fdisk` toobegin creating partitions</span></span>

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

2. <span data-ttu-id="785e9-120">Naciśnij przycisk "n" w toocreate monitu hello  **n** wa partycji:</span><span class="sxs-lookup"><span data-stu-id="785e9-120">Press 'n' at hello prompt toocreate a **n**ew partition:</span></span>

    ```bash
    Command (m for help): n
    ```

3. <span data-ttu-id="785e9-121">Następnie naciśnij klawisz "p" toocreate **p**zosta partycji:</span><span class="sxs-lookup"><span data-stu-id="785e9-121">Next, press 'p' toocreate a **p**rimary partition:</span></span>

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. <span data-ttu-id="785e9-122">Naciśnij przycisk '1' tooselect partycji o numerze 1:</span><span class="sxs-lookup"><span data-stu-id="785e9-122">Press '1' tooselect partition number 1:</span></span>

    ```bash
    Partition number (1-4): 1
    ```

5. <span data-ttu-id="785e9-123">Wybierz hello punkt początkowy hello nowej partycji lub naciśnij klawisz `<enter>` tooaccept hello domyślnej tooplace hello partycji na początku hello hello wolnego miejsca na dysku hello:</span><span class="sxs-lookup"><span data-stu-id="785e9-123">Select hello starting point of hello new partition, or press `<enter>` tooaccept hello default tooplace hello partition at hello beginning of hello free space on hello drive:</span></span>

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. <span data-ttu-id="785e9-124">Wybierz rozmiar hello hello partycji, na przykład typ "+10G" toocreate partycji 10 GB.</span><span class="sxs-lookup"><span data-stu-id="785e9-124">Select hello size of hello partition, for example type '+10G' toocreate a 10 gigabyte partition.</span></span> <span data-ttu-id="785e9-125">Możesz również nacisnąć klawisz `<enter>` Utwórz jedną partycję, obejmującej cały dysk hello:</span><span class="sxs-lookup"><span data-stu-id="785e9-125">Or, press `<enter>` create a single partition that spans hello entire drive:</span></span>

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. <span data-ttu-id="785e9-126">Następnie należy zmienić identyfikator hello i **t**ypu hello partycji z domyślnej hello IDENTYFIKATORA "83" tooID (Linux) "fd" (Linux raid automatycznie):</span><span class="sxs-lookup"><span data-stu-id="785e9-126">Next, change hello ID and **t**ype of hello partition from hello default ID '83' (Linux) tooID 'fd' (Linux raid auto):</span></span>

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L toolist codes): fd
    ```

8. <span data-ttu-id="785e9-127">Na koniec zapisu hello partycji tabeli toohello dysku i zamknąć fdisk:</span><span class="sxs-lookup"><span data-stu-id="785e9-127">Finally, write hello partition table toohello drive and exit fdisk:</span></span>

    ```bash   
    Command (m for help): w
    hello partition table has been altered!
    ```

## <a name="create-hello-raid-array"></a><span data-ttu-id="785e9-128">Tworzenie hello macierzy RAID</span><span class="sxs-lookup"><span data-stu-id="785e9-128">Create hello RAID array</span></span>
1. <span data-ttu-id="785e9-129">powitania po przykładzie zostanie "stripe" (poziom RAID 0) trzy partycji znajdujących się na trzy osobne dyski z danymi (sdc1, sdd1, sde1).</span><span class="sxs-lookup"><span data-stu-id="785e9-129">hello following example will "stripe" (RAID level 0) three partitions located on three separate data disks (sdc1, sdd1, sde1).</span></span>  <span data-ttu-id="785e9-130">Po wywołaniu metody uruchomi to polecenie nowe urządzenie RAID **/dev/md127** jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="785e9-130">After running this command a new RAID device called **/dev/md127** is created.</span></span> <span data-ttu-id="785e9-131">Należy również zauważyć, że jeśli dane te dyski możemy wcześniej częścią innego unieczynnienia macierzy RAID może być konieczne tooadd hello `--force` toohello parametru `mdadm` polecenia:</span><span class="sxs-lookup"><span data-stu-id="785e9-131">Also note that if these data disks we previously part of another defunct RAID array it may be necessary tooadd hello `--force` parameter toohello `mdadm` command:</span></span>

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. <span data-ttu-id="785e9-132">Utwórz hello system plików na powitania nowe urządzenie RAID</span><span class="sxs-lookup"><span data-stu-id="785e9-132">Create hello file system on hello new RAID device</span></span>
   
    <span data-ttu-id="785e9-133">a.</span><span class="sxs-lookup"><span data-stu-id="785e9-133">a.</span></span> <span data-ttu-id="785e9-134">**CentOS, Oracle Linux SLES 12, openSUSE i Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="785e9-134">**CentOS, Oracle Linux, SLES 12, openSUSE, and Ubuntu**</span></span>

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    <span data-ttu-id="785e9-135">b.</span><span class="sxs-lookup"><span data-stu-id="785e9-135">b.</span></span> <span data-ttu-id="785e9-136">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="785e9-136">**SLES 11**</span></span>

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    <span data-ttu-id="785e9-137">c.</span><span class="sxs-lookup"><span data-stu-id="785e9-137">c.</span></span> <span data-ttu-id="785e9-138">**SLES 11** — umożliwiają boot.md i utworzenie mdadm.conf</span><span class="sxs-lookup"><span data-stu-id="785e9-138">**SLES 11** - enable boot.md and create mdadm.conf</span></span>

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > <span data-ttu-id="785e9-139">Po wprowadzeniu zmian w systemie SUSE może być wymagane ponowne uruchomienie komputera.</span><span class="sxs-lookup"><span data-stu-id="785e9-139">A reboot may be required after making these changes on SUSE systems.</span></span> <span data-ttu-id="785e9-140">Ten krok jest *nie* wymagane na SLES 12.</span><span class="sxs-lookup"><span data-stu-id="785e9-140">This step is *not* required on SLES 12.</span></span>
   > 
   > 

## <a name="add-hello-new-file-system-tooetcfstab"></a><span data-ttu-id="785e9-141">Dodaj hello nowego pliku systemu zbyt/etc/fstab</span><span class="sxs-lookup"><span data-stu-id="785e9-141">Add hello new file system too/etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="785e9-142">Nieprawidłowo edytowania hello /etc/fstab pliku może spowodować rozruch systemu.</span><span class="sxs-lookup"><span data-stu-id="785e9-142">Improperly editing hello /etc/fstab file could result in an unbootable system.</span></span> <span data-ttu-id="785e9-143">Jeśli nie wiesz, zapoznaj się z informacji w sposób tooproperly edytować ten plik dokumentacją toohello dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="785e9-143">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="785e9-144">Zalecane jest również, że kopia zapasowa pliku /etc/fstab hello został utworzony przed rozpoczęciem edycji.</span><span class="sxs-lookup"><span data-stu-id="785e9-144">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>

1. <span data-ttu-id="785e9-145">Utwórz hello żądanego punktu instalacji do nowego systemu plików, na przykład:</span><span class="sxs-lookup"><span data-stu-id="785e9-145">Create hello desired mount point for your new file system, for example:</span></span>

    ```bash
    sudo mkdir /data
    ```
2. <span data-ttu-id="785e9-146">Podczas edytowania /etc/fstab, hello **UUID** powinny być używane tooreference hello pliku systemu zamiast hello nazwy urządzenia.</span><span class="sxs-lookup"><span data-stu-id="785e9-146">When editing /etc/fstab, hello **UUID** should be used tooreference hello file system rather than hello device name.</span></span>  <span data-ttu-id="785e9-147">Użyj hello `blkid` narzędzie toodetermine hello UUID dla hello nowy system plików:</span><span class="sxs-lookup"><span data-stu-id="785e9-147">Use hello `blkid` utility toodetermine hello UUID for hello new file system:</span></span>

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. <span data-ttu-id="785e9-148">Otwórz /etc/fstab w edytorze tekstów i Dodaj wpis dla hello nowy system plików, na przykład:</span><span class="sxs-lookup"><span data-stu-id="785e9-148">Open /etc/fstab in a text editor and add an entry for hello new file system, for example:</span></span>

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    <span data-ttu-id="785e9-149">Lub na **SLES 11**:</span><span class="sxs-lookup"><span data-stu-id="785e9-149">Or on **SLES 11**:</span></span>

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    <span data-ttu-id="785e9-150">Następnie zapisz i zamknij /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="785e9-150">Then, save and close /etc/fstab.</span></span>

4. <span data-ttu-id="785e9-151">Testowanie tego etc hello/fstab wpis jest prawidłowy:</span><span class="sxs-lookup"><span data-stu-id="785e9-151">Test that hello /etc/fstab entry is correct:</span></span>

    ```bash  
    sudo mount -a
    ```

    <span data-ttu-id="785e9-152">Jeśli to polecenie powoduje komunikat o błędzie, sprawdź, czy składnia hello w pliku /etc/fstab hello.</span><span class="sxs-lookup"><span data-stu-id="785e9-152">If this command results in an error message, please check hello syntax in hello /etc/fstab file.</span></span>
   
    <span data-ttu-id="785e9-153">Uruchom hello `mount` systemu plików hello tooensure polecenia:</span><span class="sxs-lookup"><span data-stu-id="785e9-153">Next run hello `mount` command tooensure hello file system is mounted:</span></span>

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="785e9-154">(Opcjonalnie) Parametry przed uszkodzeniami rozruchu</span><span class="sxs-lookup"><span data-stu-id="785e9-154">(Optional) Failsafe Boot Parameters</span></span>
   
    <span data-ttu-id="785e9-155">**Konfiguracja fstab**</span><span class="sxs-lookup"><span data-stu-id="785e9-155">**fstab configuration**</span></span>
   
    <span data-ttu-id="785e9-156">Wiele dystrybucji obejmują albo hello `nobootwait` lub `nofail` instalacji parametrów, które mogą być dodawane toohello/etc/fstab pliku.</span><span class="sxs-lookup"><span data-stu-id="785e9-156">Many distributions include either hello `nobootwait` or `nofail` mount parameters that may be added toohello /etc/fstab file.</span></span> <span data-ttu-id="785e9-157">Te parametry Zezwalaj na wypadek awarii w przypadku instalowania w określonym systemie plików oraz tooboot toocontinue systemu Linux hello Zezwalaj, nawet jeśli jest system plików tooproperly instalacji hello RAID.</span><span class="sxs-lookup"><span data-stu-id="785e9-157">These parameters allow for failures when mounting a particular file system and allow hello Linux system toocontinue tooboot even if it is unable tooproperly mount hello RAID file system.</span></span> <span data-ttu-id="785e9-158">Zapoznaj się z dokumentacją tooyour dystrybucji Aby uzyskać więcej informacji na temat tych parametrów.</span><span class="sxs-lookup"><span data-stu-id="785e9-158">Refer tooyour distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="785e9-159">Przykład (Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="785e9-159">Example (Ubuntu):</span></span>

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    <span data-ttu-id="785e9-160">**Parametry rozruchu systemu Linux**</span><span class="sxs-lookup"><span data-stu-id="785e9-160">**Linux boot parameters**</span></span>
   
    <span data-ttu-id="785e9-161">W dodatku toohello powyżej parametry, hello jądra parametru "`bootdegraded=true`" umożliwiają hello tooboot systemu, nawet jeśli hello RAID jest traktowany jako uszkodzony lub nieprawidłowego działania, na przykład jeśli dysk danych jest przypadkowo usunięty z maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="785e9-161">In addition toohello above parameters, hello kernel parameter "`bootdegraded=true`" can allow hello system tooboot even if hello RAID is perceived as damaged or degraded, for example if a data drive is inadvertently removed from hello virtual machine.</span></span> <span data-ttu-id="785e9-162">Domyślnie to może również spowodować-rozruchowy systemu.</span><span class="sxs-lookup"><span data-stu-id="785e9-162">By default this could also result in a non-bootable system.</span></span>
   
    <span data-ttu-id="785e9-163">Można znaleźć w dokumentacji tooyour dystrybucji w sposób tooproperly Edytuj parametry jądra.</span><span class="sxs-lookup"><span data-stu-id="785e9-163">Please refer tooyour distribution's documentation on how tooproperly edit kernel parameters.</span></span> <span data-ttu-id="785e9-164">Na przykład w wiele dystrybucji (CentOS, Oracle Linux SLES 11) tych parametrów można dodać ręcznie toohello "`/boot/grub/menu.lst`" pliku.</span><span class="sxs-lookup"><span data-stu-id="785e9-164">For example, in many distributions (CentOS, Oracle Linux, SLES 11) these parameters may be added manually toohello "`/boot/grub/menu.lst`" file.</span></span>  <span data-ttu-id="785e9-165">Na Ubuntu można dodać tego parametru toohello `GRUB_CMDLINE_LINUX_DEFAULT` zmiennej na "/ etc/domyślne/chodników".</span><span class="sxs-lookup"><span data-stu-id="785e9-165">On Ubuntu this parameter can be added toohello `GRUB_CMDLINE_LINUX_DEFAULT` variable on "/etc/default/grub".</span></span>


## <a name="trimunmap-support"></a><span data-ttu-id="785e9-166">PRZYCINANIE/UNMAP pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="785e9-166">TRIM/UNMAP support</span></span>
<span data-ttu-id="785e9-167">PRZYCINANIE/UNMAP toodiscard operacji obsługi niektóre jądra systemu Linux nieużywanych bloków na dysku hello.</span><span class="sxs-lookup"><span data-stu-id="785e9-167">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="785e9-168">Operacje te są szczególnie przydatna w tooinform standardowego magazynu Azure, po usunięciu strony nie są już prawidłowe i mogą zostać odrzucone.</span><span class="sxs-lookup"><span data-stu-id="785e9-168">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="785e9-169">Odrzucanie strony można zapisać kosztów, jeśli Tworzenie dużych plików, a następnie usuń je.</span><span class="sxs-lookup"><span data-stu-id="785e9-169">Discarding pages can save cost if you create large files and then delete them.</span></span>

> [!NOTE]
> <span data-ttu-id="785e9-170">RAID nie mogą wystawiać odrzucenia poleceń, jeśli rozmiar fragmentu hello tablicy hello ustawiono tooless niż domyślne hello (512KB).</span><span class="sxs-lookup"><span data-stu-id="785e9-170">RAID may not issue discard commands if hello chunk size for hello array is set tooless than hello default (512KB).</span></span> <span data-ttu-id="785e9-171">Jest to spowodowane Usuń mapowanie hello szczegółowości na powitania hosta jest również 512KB.</span><span class="sxs-lookup"><span data-stu-id="785e9-171">This is because hello unmap granularity on hello Host is also 512KB.</span></span> <span data-ttu-id="785e9-172">Jeśli zmodyfikowano rozmiar fragmentu hello tablicy za pomocą jego mdadm `--chunk=` parametr, a następnie usuń mapowanie/PRZYCINANIE żądania mogą być ignorowane przez hello jądra.</span><span class="sxs-lookup"><span data-stu-id="785e9-172">If you modified hello array's chunk size via mdadm's `--chunk=` parameter, then TRIM/unmap requests may be ignored by hello kernel.</span></span>

<span data-ttu-id="785e9-173">Istnieją dwa sposoby tooenable PRZYCINANIE obsługi w maszynie Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="785e9-173">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="785e9-174">W zwykły sposób poszukaj dystrybucji hello zalecane podejście:</span><span class="sxs-lookup"><span data-stu-id="785e9-174">As usual, consult your distribution for hello recommended approach:</span></span>

- <span data-ttu-id="785e9-175">Użyj hello `discard` zainstalować opcję `/etc/fstab`, na przykład:</span><span class="sxs-lookup"><span data-stu-id="785e9-175">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="785e9-176">W niektórych przypadkach hello `discard` opcji może mieć wpływ na wydajność.</span><span class="sxs-lookup"><span data-stu-id="785e9-176">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="785e9-177">Alternatywnie można uruchomić hello `fstrim` ręcznie polecenie z wiersza polecenia hello, lub dodaj je tooyour crontab toorun regularnie:</span><span class="sxs-lookup"><span data-stu-id="785e9-177">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>

    <span data-ttu-id="785e9-178">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="785e9-178">**Ubuntu**</span></span>

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    <span data-ttu-id="785e9-179">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="785e9-179">**RHEL/CentOS**</span></span>
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
