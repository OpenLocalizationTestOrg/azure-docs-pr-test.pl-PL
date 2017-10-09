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
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a><span data-ttu-id="6d4e5-103">Skonfiguruj LVM na Maszynę wirtualną systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="6d4e5-103">Configure LVM on a Linux VM in Azure</span></span>
<span data-ttu-id="6d4e5-104">Ten dokument będzie omawiać jak tooconfigure menedżera woluminu logicznego (LVM) w sieci maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-104">This document will discuss how tooconfigure Logical Volume Manager (LVM) in your Azure virtual machine.</span></span> <span data-ttu-id="6d4e5-105">Gdy jest możliwe tooconfigure LVM na dowolnym dysku dołączony toohello maszyny wirtualnej, domyślnie większość chmury obrazów nie będą miały LVM skonfigurowane na hello dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-105">While it is feasible tooconfigure LVM on any disk attached toohello virtual machine, by default most cloud images will not have LVM configured on hello OS disk.</span></span> <span data-ttu-id="6d4e5-106">To jest tooprevent problemy z grup zduplikowanych woluminu, jeśli hello dysk systemu operacyjnego jest kiedykolwiek połączona tooanother wirtualna hello tego samego dystrybucji i typ, np. podczas scenariusza odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-106">This is tooprevent problems with duplicate volume groups if hello OS disk is ever attached tooanother VM of hello same distribution and type, i.e. during a recovery scenario.</span></span> <span data-ttu-id="6d4e5-107">Dlatego zalecane jest tylko toouse LVM na powitania dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-107">Therefore it is recommended only toouse LVM on hello data disks.</span></span>

## <a name="linear-vs-striped-logical-volumes"></a><span data-ttu-id="6d4e5-108">Liniowego a woluminy rozłożone logiczne</span><span class="sxs-lookup"><span data-stu-id="6d4e5-108">Linear vs. striped logical volumes</span></span>
<span data-ttu-id="6d4e5-109">LVM mogą być używane toocombine liczbę dysków fizycznych w jednym woluminie magazynu.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-109">LVM can be used toocombine a number of physical disks into a single storage volume.</span></span> <span data-ttu-id="6d4e5-110">Domyślnie LVM zwykle utworzy liniowej woluminów logicznego, co oznacza, że łączone hello magazynu fizycznego.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-110">By default LVM will usually create linear logical volumes, which means that hello physical storage is concatenated together.</span></span> <span data-ttu-id="6d4e5-111">W takim przypadku operacji odczytu/zapisu będą zwykle wysyłane tylko jednego dysku tooa.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-111">In this case read/write operations will typically only be sent tooa single disk.</span></span> <span data-ttu-id="6d4e5-112">Z kolei firma Microsoft można utworzyć woluminy rozłożone logiczne, gdy odczyty i zapisy są dyski rozproszonej toomultiple znajdujących się w grupie woluminu hello (tj. podobne tooRAID0).</span><span class="sxs-lookup"><span data-stu-id="6d4e5-112">In contrast, we can also create striped logical volumes where reads and writes are distributed toomultiple disks contained in hello volume group (i.e. similar tooRAID0).</span></span> <span data-ttu-id="6d4e5-113">Ze względu na wydajność prawdopodobnie można toostripe logicznej woluminów tak, że odczyty i zapisy wykorzystanie dysków dołączonych danych.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-113">For performance reasons it is likely you will want toostripe your logical volumes so that reads and writes utilize all your attached data disks.</span></span>

<span data-ttu-id="6d4e5-114">Ten dokument zostanie opisano, jak toocombine danych kilka dysków w grupie pojedynczy wolumin, a następnie utwórz woluminy rozłożone logiczne.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-114">This document will describe how toocombine several data disks into a single volume group, and then create a striped logical volume.</span></span> <span data-ttu-id="6d4e5-115">Poniższe kroki Hello są nieco uogólniony toowork z większości dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-115">hello steps below are somewhat generalized toowork with most distributions.</span></span> <span data-ttu-id="6d4e5-116">W większości przypadków hello narzędzia i przepływów pracy związanych z zarządzaniem LVM na platformie Azure nie są różni się od innych środowisk.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-116">In most cases hello utilities and workflows for managing LVM on Azure are not fundamentally different than other environments.</span></span> <span data-ttu-id="6d4e5-117">W zwykły sposób również Przejrzyj dostawcą Linux dla dokumentacji i najlepsze rozwiązania dotyczące używania LVM z konkretnym dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-117">As usual, please also consult your Linux vendor for documentation and best practices for using LVM with your particular distribution.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="6d4e5-118">Dołączanie dysków z danymi</span><span class="sxs-lookup"><span data-stu-id="6d4e5-118">Attaching data disks</span></span>
<span data-ttu-id="6d4e5-119">Jeden zazwyczaj będzie toostart z co najmniej dwa dyski pusty danych przy użyciu LVM.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-119">One will usually want toostart with two or more empty data disks when using LVM.</span></span> <span data-ttu-id="6d4e5-120">Oparte na potrzeby operacji We/Wy, można wybrać tooattach dysków, które są przechowywane w naszym Standard Storage z zapasowej too500 we/wy/ps na dysku lub naszych magazyn w warstwie Premium z zapasowej too5000 we/wy/ps na dysku.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-120">Based on your IO needs, you can choose tooattach disks that are stored in our Standard Storage, with up too500 IO/ps per disk or our Premium storage with up too5000 IO/ps per disk.</span></span> <span data-ttu-id="6d4e5-121">W tym artykule nie zostaną umieszczone w szczegółów na temat tooprovision i dołączyć maszyny wirtualnej systemu Linux tooa dysków danych.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-121">This article will not go into detail on how tooprovision and attach data disks tooa Linux virtual machine.</span></span> <span data-ttu-id="6d4e5-122">Zobacz artykuł Microsoft Azure hello [podłączyć dysk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) szczegółowe informacje dotyczące sposobu tooattach pustymi danymi dysku tooa maszyny wirtualnej systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-122">Please see hello Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how tooattach an empty data disk tooa Linux virtual machine on Azure.</span></span>

## <a name="install-hello-lvm-utilities"></a><span data-ttu-id="6d4e5-123">Zainstaluj narzędzia LVM hello</span><span class="sxs-lookup"><span data-stu-id="6d4e5-123">Install hello LVM utilities</span></span>
* <span data-ttu-id="6d4e5-124">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="6d4e5-124">**Ubuntu**</span></span>

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* <span data-ttu-id="6d4e5-125">**RHEL, CentOS i Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="6d4e5-125">**RHEL, CentOS & Oracle Linux**</span></span>

    ```bash   
    sudo yum install lvm2
    ```

* <span data-ttu-id="6d4e5-126">**SLES 12 i openSUSE**</span><span class="sxs-lookup"><span data-stu-id="6d4e5-126">**SLES 12 and openSUSE**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

* <span data-ttu-id="6d4e5-127">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="6d4e5-127">**SLES 11**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

    <span data-ttu-id="6d4e5-128">Na SLES11 trzeba również edytować `/etc/sysconfig/lvm` i ustaw `LVM_ACTIVATED_ON_DISCOVERED` zbyt "Włącz":</span><span class="sxs-lookup"><span data-stu-id="6d4e5-128">On SLES11 you must also edit `/etc/sysconfig/lvm` and set `LVM_ACTIVATED_ON_DISCOVERED` too"enable":</span></span>

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a><span data-ttu-id="6d4e5-129">Konfigurowanie maszyny wirtualnej z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="6d4e5-129">Configure LVM</span></span>
<span data-ttu-id="6d4e5-130">W tym przewodniku zakładamy, że dołączono trzy dyski danych, których będziemy tooas `/dev/sdc`, `/dev/sdd` i `/dev/sde`.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-130">In this guide we will assume you have attached three data disks, which we'll refer tooas `/dev/sdc`, `/dev/sdd` and `/dev/sde`.</span></span> <span data-ttu-id="6d4e5-131">Należy pamiętać, że te nie mogą być zawsze hello tej samej nazwy ścieżki w maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-131">Note that these may not always be hello same path names in your VM.</span></span> <span data-ttu-id="6d4e5-132">Można uruchomić "`sudo fdisk -l`" lub podobne polecenie toolist dostępne dyski.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-132">You can run '`sudo fdisk -l`' or similar command toolist your available disks.</span></span>

1. <span data-ttu-id="6d4e5-133">Przygotuj woluminy fizyczne hello:</span><span class="sxs-lookup"><span data-stu-id="6d4e5-133">Prepare hello physical volumes:</span></span>

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. <span data-ttu-id="6d4e5-134">Utwórz grupę woluminu.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-134">Create a volume group.</span></span> <span data-ttu-id="6d4e5-135">W tym przykładzie wywołania hello woluminu grupy `data-vg01`:</span><span class="sxs-lookup"><span data-stu-id="6d4e5-135">In this example we are calling hello volume group `data-vg01`:</span></span>

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. <span data-ttu-id="6d4e5-136">Utwórz hello logicznej woluminów.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-136">Create hello logical volume(s).</span></span> <span data-ttu-id="6d4e5-137">Witaj możemy poniższe polecenie utworzy pojedynczy wolumin logiczną o nazwie `data-lv01` toospan hello cały wolumin grupy, ale należy pamiętać, że jest również możliwe toocreate wiele woluminów logiczne w grupie woluminu hello.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-137">hello command below we will create a single logical volume called `data-lv01` toospan hello entire volume group, but note that it is also feasible toocreate multiple logical volumes in hello volume group.</span></span>

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. <span data-ttu-id="6d4e5-138">Format hello wolumin logiczne</span><span class="sxs-lookup"><span data-stu-id="6d4e5-138">Format hello logical volume</span></span>

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > <span data-ttu-id="6d4e5-139">Z użyciem SLES11 `-t ext3` zamiast ext4.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-139">With SLES11 use `-t ext3` instead of ext4.</span></span> <span data-ttu-id="6d4e5-140">SLES11 obsługuje tylko systemy plików tooext4 dostęp tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-140">SLES11 only supports read-only access tooext4 filesystems.</span></span>

## <a name="add-hello-new-file-system-tooetcfstab"></a><span data-ttu-id="6d4e5-141">Dodaj hello nowego pliku systemu zbyt/etc/fstab</span><span class="sxs-lookup"><span data-stu-id="6d4e5-141">Add hello new file system too/etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6d4e5-142">Nieprawidłowo edycji hello `/etc/fstab` pliku może spowodować rozruch systemu.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-142">Improperly editing hello `/etc/fstab` file could result in an unbootable system.</span></span> <span data-ttu-id="6d4e5-143">Jeśli nie wiesz, można znaleźć w dokumentacji toohello dystrybucji Aby uzyskać informacje dotyczące sposobu tooproperly edytować ten plik.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-143">If unsure, please refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="6d4e5-144">Jest również zalecane kopii zapasowej hello `/etc/fstab` plik jest tworzony przed przystąpieniem do edytowania.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-144">It is also recommended that a backup of hello `/etc/fstab` file is created before editing.</span></span>

1. <span data-ttu-id="6d4e5-145">Utwórz hello żądanego punktu instalacji do nowego systemu plików, na przykład:</span><span class="sxs-lookup"><span data-stu-id="6d4e5-145">Create hello desired mount point for your new file system, for example:</span></span>

    ```bash  
    sudo mkdir /data
    ```

2. <span data-ttu-id="6d4e5-146">Znajdź ścieżki woluminu logicznego hello</span><span class="sxs-lookup"><span data-stu-id="6d4e5-146">Locate hello logical volume path</span></span>

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. <span data-ttu-id="6d4e5-147">Otwórz `/etc/fstab` w edytorze tekstów i Dodaj wpis dla hello nowy system plików, na przykład:</span><span class="sxs-lookup"><span data-stu-id="6d4e5-147">Open `/etc/fstab` in a text editor and add an entry for hello new file system, for example:</span></span>

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    <span data-ttu-id="6d4e5-148">Następnie zapisz i Zamknij `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-148">Then, save and close `/etc/fstab`.</span></span>

4. <span data-ttu-id="6d4e5-149">Testowanie tego hello `/etc/fstab` wpis jest prawidłowy:</span><span class="sxs-lookup"><span data-stu-id="6d4e5-149">Test that hello `/etc/fstab` entry is correct:</span></span>

    ```bash    
    sudo mount -a
    ```

    <span data-ttu-id="6d4e5-150">Jeśli to polecenie powoduje komunikat o błędzie Sprawdź składnię hello hello `/etc/fstab` pliku.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-150">If this command results in an error message please check hello syntax in hello `/etc/fstab` file.</span></span>
   
    <span data-ttu-id="6d4e5-151">Uruchom hello `mount` systemu plików hello tooensure polecenia:</span><span class="sxs-lookup"><span data-stu-id="6d4e5-151">Next run hello `mount` command tooensure hello file system is mounted:</span></span>

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="6d4e5-152">(Opcjonalnie) Parametry rozruchu przed uszkodzeniami w`/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="6d4e5-152">(Optional) Failsafe boot parameters in `/etc/fstab`</span></span>
   
    <span data-ttu-id="6d4e5-153">Wiele dystrybucji obejmują albo hello `nobootwait` lub `nofail` zainstalować parametrów, które mogą być dodawane toohello `/etc/fstab` pliku.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-153">Many distributions include either hello `nobootwait` or `nofail` mount parameters that may be added toohello `/etc/fstab` file.</span></span> <span data-ttu-id="6d4e5-154">Te parametry Zezwalaj na wypadek awarii w przypadku instalowania w określonym systemie plików oraz tooboot toocontinue systemu Linux hello Zezwalaj, nawet jeśli jest system plików tooproperly instalacji hello RAID.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-154">These parameters allow for failures when mounting a particular file system and allow hello Linux system toocontinue tooboot even if it is unable tooproperly mount hello RAID file system.</span></span> <span data-ttu-id="6d4e5-155">Aby uzyskać więcej informacji na temat tych parametrów, zapoznaj się z dokumentacją tooyour dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-155">Please refer tooyour distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="6d4e5-156">Przykład (Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="6d4e5-156">Example (Ubuntu):</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a><span data-ttu-id="6d4e5-157">PRZYCINANIE/UNMAP pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="6d4e5-157">TRIM/UNMAP support</span></span>
<span data-ttu-id="6d4e5-158">PRZYCINANIE/UNMAP toodiscard operacji obsługi niektóre jądra systemu Linux nieużywanych bloków na dysku hello.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-158">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="6d4e5-159">Operacje te są szczególnie przydatna w tooinform standardowego magazynu Azure, po usunięciu strony nie są już prawidłowe i mogą zostać odrzucone.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-159">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="6d4e5-160">Odrzucanie strony można zapisać kosztów, jeśli Tworzenie dużych plików, a następnie usuń je.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-160">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="6d4e5-161">Istnieją dwa sposoby tooenable PRZYCINANIE obsługi w maszynie Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-161">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="6d4e5-162">W zwykły sposób poszukaj dystrybucji hello zalecane podejście:</span><span class="sxs-lookup"><span data-stu-id="6d4e5-162">As usual, consult your distribution for hello recommended approach:</span></span>

- <span data-ttu-id="6d4e5-163">Użyj hello `discard` zainstalować opcję `/etc/fstab`, na przykład:</span><span class="sxs-lookup"><span data-stu-id="6d4e5-163">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="6d4e5-164">W niektórych przypadkach hello `discard` opcji może mieć wpływ na wydajność.</span><span class="sxs-lookup"><span data-stu-id="6d4e5-164">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="6d4e5-165">Alternatywnie można uruchomić hello `fstrim` ręcznie polecenie z wiersza polecenia hello, lub dodaj je tooyour crontab toorun regularnie:</span><span class="sxs-lookup"><span data-stu-id="6d4e5-165">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>

    <span data-ttu-id="6d4e5-166">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="6d4e5-166">**Ubuntu**</span></span>

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    <span data-ttu-id="6d4e5-167">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="6d4e5-167">**RHEL/CentOS**</span></span>

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
