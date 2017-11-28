---
title: "Należy skonfigurować oprogramowanie RAID na maszynie wirtualnej z systemem Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować RAID w systemie Linux na platformie Azure przy użyciu mdadm."
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
ms.openlocfilehash: 12f540a700fbf85e579e8aadc9f6def039299ff7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-software-raid-on-linux"></a><span data-ttu-id="f42bb-103">Konfigurowanie macierzy RAID oprogramowania w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="f42bb-103">Configure Software RAID on Linux</span></span>
<span data-ttu-id="f42bb-104">Jest to typowy scenariusz, aby korzystać z oprogramowania RAID na maszynach wirtualnych systemu Linux na platformie Azure można prezentować wiele dysków dołączonych danych jako pojedynczego urządzenia RAID.</span><span class="sxs-lookup"><span data-stu-id="f42bb-104">It's a common scenario to use software RAID on Linux virtual machines in Azure to present multiple attached data disks as a single RAID device.</span></span> <span data-ttu-id="f42bb-105">Zazwyczaj może być używany do zwiększenia wydajności i umożliwiają lepsze przepustowości w porównaniu do przy użyciu jednego dysku.</span><span class="sxs-lookup"><span data-stu-id="f42bb-105">Typically this can be used to improve performance and allow for improved throughput compared to using just a single disk.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="f42bb-106">Dołączanie dysków z danymi</span><span class="sxs-lookup"><span data-stu-id="f42bb-106">Attaching data disks</span></span>
<span data-ttu-id="f42bb-107">Co najmniej dwa dyski danych puste są potrzebne do skonfigurowania urządzenie RAID.</span><span class="sxs-lookup"><span data-stu-id="f42bb-107">Two or more empty data disks are needed to configure a RAID device.</span></span>  <span data-ttu-id="f42bb-108">Jest główną przyczyną tworzenia urządzenia RAID poprawić wydajność We/Wy dysku.</span><span class="sxs-lookup"><span data-stu-id="f42bb-108">The primary reason for creating a RAID device is to improve performance of your disk IO.</span></span>  <span data-ttu-id="f42bb-109">Oparte na potrzeby operacji We/Wy, można dołączać dysków, które są przechowywane w naszym Standard Storage z maksymalnie 500 we/wy/ps na dysku lub naszych Premium storage z maksymalnie 5000 ps/we/wy na dysk.</span><span class="sxs-lookup"><span data-stu-id="f42bb-109">Based on your IO needs, you can choose to attach disks that are stored in our Standard Storage, with up to 500 IO/ps per disk or our Premium storage with up to 5000 IO/ps per disk.</span></span> <span data-ttu-id="f42bb-110">W tym artykule nie przejść do szczegółów na temat obsługi administracyjnej i dołączać dysków z danymi do maszyny wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="f42bb-110">This article does not go into detail on how to provision and attach data disks to a Linux virtual machine.</span></span>  <span data-ttu-id="f42bb-111">Zapoznaj się z artykułem Microsoft Azure [podłączyć dysk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) szczegółowe informacje o tym, jak można dołączyć dysku danych puste do maszyny wirtualnej systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f42bb-111">See the Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how to attach an empty data disk to a Linux virtual machine on Azure.</span></span>

## <a name="install-the-mdadm-utility"></a><span data-ttu-id="f42bb-112">Zainstaluj narzędzie mdadm</span><span class="sxs-lookup"><span data-stu-id="f42bb-112">Install the mdadm utility</span></span>
* <span data-ttu-id="f42bb-113">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="f42bb-113">**Ubuntu**</span></span>
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* <span data-ttu-id="f42bb-114">**CentOS & Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="f42bb-114">**CentOS & Oracle Linux**</span></span>
```bash
sudo yum install mdadm
```

* <span data-ttu-id="f42bb-115">**SLES i openSUSE**</span><span class="sxs-lookup"><span data-stu-id="f42bb-115">**SLES and openSUSE**</span></span>
```bash  
zypper install mdadm
```

## <a name="create-the-disk-partitions"></a><span data-ttu-id="f42bb-116">Tworzenie partycji dysku</span><span class="sxs-lookup"><span data-stu-id="f42bb-116">Create the disk partitions</span></span>
<span data-ttu-id="f42bb-117">W tym przykładzie tworzymy partycji jednego dysku na /dev/sdc.</span><span class="sxs-lookup"><span data-stu-id="f42bb-117">In this example, we create a single disk partition on /dev/sdc.</span></span> <span data-ttu-id="f42bb-118">/Dev/sdc1 zostanie wywołana nową partycję dysku.</span><span class="sxs-lookup"><span data-stu-id="f42bb-118">The new disk partition will be called /dev/sdc1.</span></span>

1. <span data-ttu-id="f42bb-119">Uruchom `fdisk` aby rozpocząć tworzenie partycji</span><span class="sxs-lookup"><span data-stu-id="f42bb-119">Start `fdisk` to begin creating partitions</span></span>

    ```bash
    sudo fdisk /dev/sdc
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0xa34cb70c.
    Changes will remain in memory only, until you decide to write them.
    After that, of course, the previous content won't be recoverable.

    WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
                    switch off the mode (command 'c') and change display units to
                    sectors (command 'u').
    ```

2. <span data-ttu-id="f42bb-120">Naciśnij przycisk "n" w wierszu polecenia, aby utworzyć  **n** wa partycji:</span><span class="sxs-lookup"><span data-stu-id="f42bb-120">Press 'n' at the prompt to create a **n**ew partition:</span></span>

    ```bash
    Command (m for help): n
    ```

3. <span data-ttu-id="f42bb-121">Następnie naciśnij klawisz p, aby utworzyć **p**zosta partycji:</span><span class="sxs-lookup"><span data-stu-id="f42bb-121">Next, press 'p' to create a **p**rimary partition:</span></span>

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. <span data-ttu-id="f42bb-122">Naciśnij "1", aby wybrać numer partycji 1:</span><span class="sxs-lookup"><span data-stu-id="f42bb-122">Press '1' to select partition number 1:</span></span>

    ```bash
    Partition number (1-4): 1
    ```

5. <span data-ttu-id="f42bb-123">Wybierz punkt początkowy nową partycję, lub naciśnij przycisk `<enter>` aby zaakceptować ustawienie domyślne można umieścić na początku ilość wolnego miejsca na dysku partycji:</span><span class="sxs-lookup"><span data-stu-id="f42bb-123">Select the starting point of the new partition, or press `<enter>` to accept the default to place the partition at the beginning of the free space on the drive:</span></span>

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. <span data-ttu-id="f42bb-124">Wybierz rozmiar partycji, na przykład wpisz +10G, aby utworzyć partycję 10 GB.</span><span class="sxs-lookup"><span data-stu-id="f42bb-124">Select the size of the partition, for example type '+10G' to create a 10 gigabyte partition.</span></span> <span data-ttu-id="f42bb-125">Możesz również nacisnąć klawisz `<enter>` Utwórz jedną partycję, która obejmuje cały dysk:</span><span class="sxs-lookup"><span data-stu-id="f42bb-125">Or, press `<enter>` create a single partition that spans the entire drive:</span></span>

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. <span data-ttu-id="f42bb-126">Następnie należy zmienić identyfikator i **t**typ partycji z domyślny identyfikator "83" (Linux) do Identyfikatora "fd" (Linux raid automatycznie):</span><span class="sxs-lookup"><span data-stu-id="f42bb-126">Next, change the ID and **t**ype of the partition from the default ID '83' (Linux) to ID 'fd' (Linux raid auto):</span></span>

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L to list codes): fd
    ```

8. <span data-ttu-id="f42bb-127">Na koniec zapisu tabeli partycji na dysku i zamknąć fdisk:</span><span class="sxs-lookup"><span data-stu-id="f42bb-127">Finally, write the partition table to the drive and exit fdisk:</span></span>

    ```bash   
    Command (m for help): w
    The partition table has been altered!
    ```

## <a name="create-the-raid-array"></a><span data-ttu-id="f42bb-128">Tworzenie macierzy RAID</span><span class="sxs-lookup"><span data-stu-id="f42bb-128">Create the RAID array</span></span>
1. <span data-ttu-id="f42bb-129">Następujący przykład będzie "stripe" (poziom RAID 0) trzy partycji znajdujących się na trzy osobne dyski z danymi (sdc1, sdd1, sde1).</span><span class="sxs-lookup"><span data-stu-id="f42bb-129">The following example will "stripe" (RAID level 0) three partitions located on three separate data disks (sdc1, sdd1, sde1).</span></span>  <span data-ttu-id="f42bb-130">Po wywołaniu metody uruchomi to polecenie nowe urządzenie RAID **/dev/md127** jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="f42bb-130">After running this command a new RAID device called **/dev/md127** is created.</span></span> <span data-ttu-id="f42bb-131">Należy również zauważyć, że jeśli dane te dyski możemy wcześniej częścią innego unieczynnienia macierzy RAID może być konieczne dodanie `--force` parametr `mdadm` polecenia:</span><span class="sxs-lookup"><span data-stu-id="f42bb-131">Also note that if these data disks we previously part of another defunct RAID array it may be necessary to add the `--force` parameter to the `mdadm` command:</span></span>

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. <span data-ttu-id="f42bb-132">Utwórz system plików na nowe urządzenie RAID</span><span class="sxs-lookup"><span data-stu-id="f42bb-132">Create the file system on the new RAID device</span></span>
   
    <span data-ttu-id="f42bb-133">a.</span><span class="sxs-lookup"><span data-stu-id="f42bb-133">a.</span></span> <span data-ttu-id="f42bb-134">**CentOS, Oracle Linux SLES 12, openSUSE i Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="f42bb-134">**CentOS, Oracle Linux, SLES 12, openSUSE, and Ubuntu**</span></span>

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    <span data-ttu-id="f42bb-135">b.</span><span class="sxs-lookup"><span data-stu-id="f42bb-135">b.</span></span> <span data-ttu-id="f42bb-136">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="f42bb-136">**SLES 11**</span></span>

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    <span data-ttu-id="f42bb-137">c.</span><span class="sxs-lookup"><span data-stu-id="f42bb-137">c.</span></span> <span data-ttu-id="f42bb-138">**SLES 11** — umożliwiają boot.md i utworzenie mdadm.conf</span><span class="sxs-lookup"><span data-stu-id="f42bb-138">**SLES 11** - enable boot.md and create mdadm.conf</span></span>

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > <span data-ttu-id="f42bb-139">Po wprowadzeniu zmian w systemie SUSE może być wymagane ponowne uruchomienie komputera.</span><span class="sxs-lookup"><span data-stu-id="f42bb-139">A reboot may be required after making these changes on SUSE systems.</span></span> <span data-ttu-id="f42bb-140">Ten krok jest *nie* wymagane na SLES 12.</span><span class="sxs-lookup"><span data-stu-id="f42bb-140">This step is *not* required on SLES 12.</span></span>
   > 
   > 

## <a name="add-the-new-file-system-to-etcfstab"></a><span data-ttu-id="f42bb-141">Dodaj nowy system plików do /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="f42bb-141">Add the new file system to /etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f42bb-142">Nieprawidłowo edytowania pliku /etc/fstab może spowodować rozruch systemu.</span><span class="sxs-lookup"><span data-stu-id="f42bb-142">Improperly editing the /etc/fstab file could result in an unbootable system.</span></span> <span data-ttu-id="f42bb-143">Jeśli nie wiesz, można znaleźć dystrybucji dokumentacji, aby uzyskać informacje dotyczące prawidłowo edytować ten plik.</span><span class="sxs-lookup"><span data-stu-id="f42bb-143">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="f42bb-144">Zalecane jest również, że kopia zapasowa pliku /etc/fstab został utworzony przed przystąpieniem do edytowania.</span><span class="sxs-lookup"><span data-stu-id="f42bb-144">It is also recommended that a backup of the /etc/fstab file is created before editing.</span></span>

1. <span data-ttu-id="f42bb-145">Utwórz punkt instalacji odpowiednią dla nowego systemu plików, na przykład:</span><span class="sxs-lookup"><span data-stu-id="f42bb-145">Create the desired mount point for your new file system, for example:</span></span>

    ```bash
    sudo mkdir /data
    ```
2. <span data-ttu-id="f42bb-146">Podczas edytowania /etc/fstab, **UUID** należy odwoływać się do systemu plików, a nie do nazwy urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f42bb-146">When editing /etc/fstab, the **UUID** should be used to reference the file system rather than the device name.</span></span>  <span data-ttu-id="f42bb-147">Użyj `blkid` narzędzie, aby określić identyfikator UUID dla nowego systemu plików:</span><span class="sxs-lookup"><span data-stu-id="f42bb-147">Use the `blkid` utility to determine the UUID for the new file system:</span></span>

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. <span data-ttu-id="f42bb-148">Otwórz /etc/fstab w edytorze tekstów i Dodaj wpis dla nowego systemu plików, na przykład:</span><span class="sxs-lookup"><span data-stu-id="f42bb-148">Open /etc/fstab in a text editor and add an entry for the new file system, for example:</span></span>

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    <span data-ttu-id="f42bb-149">Lub na **SLES 11**:</span><span class="sxs-lookup"><span data-stu-id="f42bb-149">Or on **SLES 11**:</span></span>

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    <span data-ttu-id="f42bb-150">Następnie zapisz i zamknij /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="f42bb-150">Then, save and close /etc/fstab.</span></span>

4. <span data-ttu-id="f42bb-151">Testowanie, czy/etc/fstab wpis jest poprawny:</span><span class="sxs-lookup"><span data-stu-id="f42bb-151">Test that the /etc/fstab entry is correct:</span></span>

    ```bash  
    sudo mount -a
    ```

    <span data-ttu-id="f42bb-152">Jeśli to polecenie powoduje komunikat o błędzie, Sprawdź składnię pliku /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="f42bb-152">If this command results in an error message, please check the syntax in the /etc/fstab file.</span></span>
   
    <span data-ttu-id="f42bb-153">Uruchom `mount` polecenie, aby upewnić się, systemu plików:</span><span class="sxs-lookup"><span data-stu-id="f42bb-153">Next run the `mount` command to ensure the file system is mounted:</span></span>

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="f42bb-154">(Opcjonalnie) Parametry przed uszkodzeniami rozruchu</span><span class="sxs-lookup"><span data-stu-id="f42bb-154">(Optional) Failsafe Boot Parameters</span></span>
   
    <span data-ttu-id="f42bb-155">**Konfiguracja fstab**</span><span class="sxs-lookup"><span data-stu-id="f42bb-155">**fstab configuration**</span></span>
   
    <span data-ttu-id="f42bb-156">Zawiera wiele dystrybucji `nobootwait` lub `nofail` parametrów, które mogą być dodawane do pliku/etc/fstab instalacji.</span><span class="sxs-lookup"><span data-stu-id="f42bb-156">Many distributions include either the `nobootwait` or `nofail` mount parameters that may be added to the /etc/fstab file.</span></span> <span data-ttu-id="f42bb-157">Te parametry Zezwalaj na wypadek awarii w przypadku instalowania w określonym systemie plików i Zezwalaj na systemie Linux, aby kontynuować do rozruchu, nawet jeśli nie można poprawnie zainstalować system plików woluminu macierzy RAID.</span><span class="sxs-lookup"><span data-stu-id="f42bb-157">These parameters allow for failures when mounting a particular file system and allow the Linux system to continue to boot even if it is unable to properly mount the RAID file system.</span></span> <span data-ttu-id="f42bb-158">Zajrzyj do dokumentacji programu dystrybucji, aby uzyskać więcej informacji na temat tych parametrów.</span><span class="sxs-lookup"><span data-stu-id="f42bb-158">Refer to your distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="f42bb-159">Przykład (Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="f42bb-159">Example (Ubuntu):</span></span>

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    <span data-ttu-id="f42bb-160">**Parametry rozruchu systemu Linux**</span><span class="sxs-lookup"><span data-stu-id="f42bb-160">**Linux boot parameters**</span></span>
   
    <span data-ttu-id="f42bb-161">Oprócz powyższych parametrów parametru jądra "`bootdegraded=true`" można zezwolić na system przeprowadzić rozruch nawet wtedy, gdy RAID jest traktowany jako uszkodzony lub obniżeniem, aby uzyskać przykład, jeśli dysk danych zostanie przypadkowo usunięty z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f42bb-161">In addition to the above parameters, the kernel parameter "`bootdegraded=true`" can allow the system to boot even if the RAID is perceived as damaged or degraded, for example if a data drive is inadvertently removed from the virtual machine.</span></span> <span data-ttu-id="f42bb-162">Domyślnie to może również spowodować-rozruchowy systemu.</span><span class="sxs-lookup"><span data-stu-id="f42bb-162">By default this could also result in a non-bootable system.</span></span>
   
    <span data-ttu-id="f42bb-163">Zapoznaj się z dystrybucji dokumentacji na temat sposobu prawidłowo Edytuj parametry jądra.</span><span class="sxs-lookup"><span data-stu-id="f42bb-163">Please refer to your distribution's documentation on how to properly edit kernel parameters.</span></span> <span data-ttu-id="f42bb-164">Na przykład w wiele dystrybucji (CentOS, Oracle Linux SLES 11) tych parametrów można dodać ręcznie do "`/boot/grub/menu.lst`" pliku.</span><span class="sxs-lookup"><span data-stu-id="f42bb-164">For example, in many distributions (CentOS, Oracle Linux, SLES 11) these parameters may be added manually to the "`/boot/grub/menu.lst`" file.</span></span>  <span data-ttu-id="f42bb-165">Na Ubuntu można dodać do tego parametru `GRUB_CMDLINE_LINUX_DEFAULT` zmiennej na "/ etc/domyślne/chodników".</span><span class="sxs-lookup"><span data-stu-id="f42bb-165">On Ubuntu this parameter can be added to the `GRUB_CMDLINE_LINUX_DEFAULT` variable on "/etc/default/grub".</span></span>


## <a name="trimunmap-support"></a><span data-ttu-id="f42bb-166">PRZYCINANIE/UNMAP pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="f42bb-166">TRIM/UNMAP support</span></span>
<span data-ttu-id="f42bb-167">Niektóre jądra systemu Linux obsługują PRZYCINANIE/UNMAP operacji Odrzuć nieużywanych bloków na dysku.</span><span class="sxs-lookup"><span data-stu-id="f42bb-167">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="f42bb-168">Operacje te są szczególnie przydatna w standardowe magazynu Azure, po usunięciu strony nie są już prawidłowe i mogą zostać odrzucone.</span><span class="sxs-lookup"><span data-stu-id="f42bb-168">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="f42bb-169">Odrzucanie strony można zapisać kosztów, jeśli Tworzenie dużych plików, a następnie usuń je.</span><span class="sxs-lookup"><span data-stu-id="f42bb-169">Discarding pages can save cost if you create large files and then delete them.</span></span>

> [!NOTE]
> <span data-ttu-id="f42bb-170">RAID nie mogą wystawiać odrzucenia polecenia, jeśli rozmiar segmentu tablicy ma ustawioną wartość mniejszą niż domyślne (512KB).</span><span class="sxs-lookup"><span data-stu-id="f42bb-170">RAID may not issue discard commands if the chunk size for the array is set to less than the default (512KB).</span></span> <span data-ttu-id="f42bb-171">Jest to spowodowane szczegółowości unmap na hoście jest również 512KB.</span><span class="sxs-lookup"><span data-stu-id="f42bb-171">This is because the unmap granularity on the Host is also 512KB.</span></span> <span data-ttu-id="f42bb-172">Jeśli zmodyfikowano rozmiar fragmentu tablicy za pomocą jego mdadm `--chunk=` parametr, a następnie usuń mapowanie/PRZYCINANIE żądań można zignorować przez jądro.</span><span class="sxs-lookup"><span data-stu-id="f42bb-172">If you modified the array's chunk size via mdadm's `--chunk=` parameter, then TRIM/unmap requests may be ignored by the kernel.</span></span>

<span data-ttu-id="f42bb-173">Istnieją dwa sposoby, aby umożliwić PRZYCINANIE obsługi w maszynie Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="f42bb-173">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="f42bb-174">W zwykły sposób poszukaj dystrybucji zalecane podejście:</span><span class="sxs-lookup"><span data-stu-id="f42bb-174">As usual, consult your distribution for the recommended approach:</span></span>

- <span data-ttu-id="f42bb-175">Użyj `discard` zainstalować opcję `/etc/fstab`, na przykład:</span><span class="sxs-lookup"><span data-stu-id="f42bb-175">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="f42bb-176">W niektórych przypadkach `discard` opcji może mieć wpływ na wydajność.</span><span class="sxs-lookup"><span data-stu-id="f42bb-176">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="f42bb-177">Alternatywnie można uruchomić `fstrim` ręcznie polecenie w wierszu polecenia lub dodać go do Twojego crontab regularnego uruchamiania:</span><span class="sxs-lookup"><span data-stu-id="f42bb-177">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>

    <span data-ttu-id="f42bb-178">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="f42bb-178">**Ubuntu**</span></span>

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    <span data-ttu-id="f42bb-179">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="f42bb-179">**RHEL/CentOS**</span></span>
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
