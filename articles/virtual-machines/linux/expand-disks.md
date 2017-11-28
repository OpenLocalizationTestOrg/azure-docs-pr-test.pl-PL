---
title: "wirtualne dyski twarde aaaExpand na Maszynę wirtualną systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wirtualne dyski twarde tooexpand na Maszynę wirtualną systemu Linux z hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: 7c09a682cb4322c027e57667640e8f1f8e6612f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooexpand-virtual-hard-disks-on-a-linux-vm-with-hello-azure-cli"></a><span data-ttu-id="26126-103">Jak wirtualne dyski twarde tooexpand na Maszynę wirtualną systemu Linux z hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="26126-103">How tooexpand virtual hard disks on a Linux VM with hello Azure CLI</span></span>
<span data-ttu-id="26126-104">Witaj domyślny rozmiar wirtualnego dysku twardego systemu operacyjnego hello (systemu operacyjnego) jest zwykle 30 GB na maszynie wirtualnej systemu Linux (VM) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="26126-104">hello default virtual hard disk size for hello operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="26126-105">Możesz [Dodaj dyski danych](add-disk.md) tooprovide dla dodatkowego miejsca, ale może również określić tooexpand istniejącego dysku danych.</span><span class="sxs-lookup"><span data-stu-id="26126-105">You can [add data disks](add-disk.md) tooprovide for additional storage space, but you may also wish tooexpand an existing data disk.</span></span> <span data-ttu-id="26126-106">Ten artykuł zawiera szczegóły dotyczące sposobu zarządzania tooexpand dysków maszyny wirtualnej systemu Linux z hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="26126-106">This article details how tooexpand managed disks for a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="26126-107">Można również rozszerzać dysk systemu operacyjnego hello niezarządzanych z hello [Azure CLI 1.0](expand-disks-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="26126-107">You can also expand hello unmanaged OS disk with hello [Azure CLI 1.0](expand-disks-nodejs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="26126-108">Zawsze upewnij się, utworzono kopię zapasową danych przed wykonaniem dysku zmienić rozmiar operacji.</span><span class="sxs-lookup"><span data-stu-id="26126-108">Always make sure that you back up your data before you perform disk resize operations.</span></span> <span data-ttu-id="26126-109">Aby uzyskać więcej informacji, zobacz [kopii zapasowych maszyn wirtualnych systemu Linux na platformie Azure](tutorial-backup-vms.md).</span><span class="sxs-lookup"><span data-stu-id="26126-109">For more information, see [Back up Linux VMs in Azure](tutorial-backup-vms.md).</span></span>

## <a name="expand-disk"></a><span data-ttu-id="26126-110">Zwiększ rozmiar dysku</span><span class="sxs-lookup"><span data-stu-id="26126-110">Expand disk</span></span>
<span data-ttu-id="26126-111">Upewnij się, że ma hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="26126-111">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="26126-112">W tym artykule wymaga istniejącej maszyny Wirtualnej na platformie Azure z co najmniej jeden dysk danych dołączona i przygotowane.</span><span class="sxs-lookup"><span data-stu-id="26126-112">This article requires an existing VM in Azure with at least one data disk attached and prepared.</span></span> <span data-ttu-id="26126-113">Jeśli nie masz już maszyny Wirtualnej, który można użyć, zobacz [tworzenie i przygotowywanie maszyny Wirtualnej z dyskami danych](tutorial-manage-disks.md#create-and-attach-disks).</span><span class="sxs-lookup"><span data-stu-id="26126-113">If you do not already have a VM that you can use, see [Create and prepare a VM with data disks](tutorial-manage-disks.md#create-and-attach-disks).</span></span>

<span data-ttu-id="26126-114">Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="26126-114">In hello following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="26126-115">Przykład nazwy parametru zawierają *myResourceGroup* i *myVM*.</span><span class="sxs-lookup"><span data-stu-id="26126-115">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

1. <span data-ttu-id="26126-116">Nie można wykonać operacji na wirtualnych dyskach twardych z hello wirtualna uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="26126-116">Operations on virtual hard disks cannot be performed with hello VM running.</span></span> <span data-ttu-id="26126-117">Cofnięcie przydziału maszyny Wirtualnej z [deallocate wirtualna az](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="26126-117">Deallocate your VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="26126-118">Witaj poniższy przykład cofa alokację hello maszyny Wirtualnej o nazwie *myVM* hello grupy zasobów o nazwie *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="26126-118">hello following example deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="26126-119">`az vm stop`zwalnia zasoby obliczeniowe hello.</span><span class="sxs-lookup"><span data-stu-id="26126-119">`az vm stop` does not release hello compute resources.</span></span> <span data-ttu-id="26126-120">toorelease zasoby obliczeniowe, użyj `az vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="26126-120">toorelease compute resources, use `az vm deallocate`.</span></span> <span data-ttu-id="26126-121">Witaj maszyny Wirtualnej można cofnąć przydziału tooexpand hello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="26126-121">hello VM must be deallocated tooexpand hello virtual hard disk.</span></span>

2. <span data-ttu-id="26126-122">Wyświetl listę dysków zarządzanych w grupie zasobów o [Lista dysków az](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="26126-122">View a list of managed disks in a resource group with [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="26126-123">Hello poniższym przykładzie zostanie wyświetlona lista dysków zarządzanych w grupie zasobów hello o nazwie *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="26126-123">hello following example displays a list of managed disks in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    <span data-ttu-id="26126-124">Zwiększ rozmiar dysku wymagana hello z [aktualizacja dysku az](/cli/azure/disk#update).</span><span class="sxs-lookup"><span data-stu-id="26126-124">Expand hello required disk with [az disk update](/cli/azure/disk#update).</span></span> <span data-ttu-id="26126-125">Witaj poniższy przykład rozszerza hello dysków zarządzanych o nazwie *myDataDisk* toobe *200*rozmiar Gb:</span><span class="sxs-lookup"><span data-stu-id="26126-125">hello following example expands hello managed disk named *myDataDisk* toobe *200*Gb in size:</span></span>

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > <span data-ttu-id="26126-126">Po rozwinięciu dysków zarządzanych hello zaktualizowano rozmiar jest mapowane toohello najbliższego rozmiaru dysków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="26126-126">When you expand a managed disk, hello updated size is mapped toohello nearest managed disk size.</span></span> <span data-ttu-id="26126-127">Dla tabeli hello dysków zarządzanych w dostępne rozmiary i warstw, zobacz [Azure zarządzanych dysków Przegląd — cennik i rozliczenia](../windows/managed-disks-overview.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="26126-127">For a table of hello available managed disk sizes and tiers, see [Azure Managed Disks Overview - Pricing and Billing](../windows/managed-disks-overview.md#pricing-and-billing).</span></span>

3. <span data-ttu-id="26126-128">Uruchom maszyny Wirtualnej z [uruchomienia maszyny wirtualnej az](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="26126-128">Start your VM with [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="26126-129">Po uruchomieniu przykład Hello hello maszyny Wirtualnej o nazwie *myVM* hello grupy zasobów o nazwie *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="26126-129">hello following example starts hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="26126-130">Tooyour SSH maszyny Wirtualnej z hello odpowiednie poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="26126-130">SSH tooyour VM with hello appropriate credentials.</span></span> <span data-ttu-id="26126-131">Możesz uzyskać hello publicznego adresu IP maszyny Wirtualnej z [az maszyny wirtualnej pokazu](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="26126-131">You can obtain hello public IP address of your VM with [az vm show](/cli/azure/vm#show):</span></span>

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. <span data-ttu-id="26126-132">toouse hello rozwinięty dysku, należy partycji podstawowej hello tooexpand i systemu plików.</span><span class="sxs-lookup"><span data-stu-id="26126-132">toouse hello expanded disk, you need tooexpand hello underlying partition and filesystem.</span></span>

    <span data-ttu-id="26126-133">a.</span><span class="sxs-lookup"><span data-stu-id="26126-133">a.</span></span> <span data-ttu-id="26126-134">Jeśli już zainstalowane, odinstaluj hello dysku:</span><span class="sxs-lookup"><span data-stu-id="26126-134">If already mounted, unmount hello disk:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

    <span data-ttu-id="26126-135">b.</span><span class="sxs-lookup"><span data-stu-id="26126-135">b.</span></span> <span data-ttu-id="26126-136">Użyj `parted` tooview informacje o dysku i rozmiar partycji hello:</span><span class="sxs-lookup"><span data-stu-id="26126-136">Use `parted` tooview disk information and resize hello partition:</span></span>

    ```bash
    sudo parted /dev/sdc
    ```

    <span data-ttu-id="26126-137">Wyświetl informacje o hello istniejący układ partycji z `print`.</span><span class="sxs-lookup"><span data-stu-id="26126-137">View information about hello existing partition layout with `print`.</span></span> <span data-ttu-id="26126-138">Witaj danych wyjściowych jest podobne toohello poniższy przykład, który zawiera informacje o dysku hello 215 Gb ma rozmiar:</span><span class="sxs-lookup"><span data-stu-id="26126-138">hello output is similar toohello following example, which shows hello underlying disk is 215Gb in size:</span></span>

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome tooGNU Parted! Type 'help' tooview a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    <span data-ttu-id="26126-139">c.</span><span class="sxs-lookup"><span data-stu-id="26126-139">c.</span></span> <span data-ttu-id="26126-140">Rozwiń węzeł hello partycji o `resizepart`.</span><span class="sxs-lookup"><span data-stu-id="26126-140">Expand hello partition with `resizepart`.</span></span> <span data-ttu-id="26126-141">Wprowadź numer partycji hello, *1*i rozmiaru dla nowej partycji hello:</span><span class="sxs-lookup"><span data-stu-id="26126-141">Enter hello partition number, *1*, and a size for hello new partition:</span></span>

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    <span data-ttu-id="26126-142">d.</span><span class="sxs-lookup"><span data-stu-id="26126-142">d.</span></span> <span data-ttu-id="26126-143">tooexit, wprowadź`quit`</span><span class="sxs-lookup"><span data-stu-id="26126-143">tooexit, enter `quit`</span></span>

5. <span data-ttu-id="26126-144">Z partycją hello zmiany rozmiaru, należy sprawdzić spójność partycji hello z `e2fsck`:</span><span class="sxs-lookup"><span data-stu-id="26126-144">With hello partition resized, verify hello partition consistency with `e2fsck`:</span></span>

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. <span data-ttu-id="26126-145">Teraz Zmień rozmiar filesystem hello z `resize2fs`:</span><span class="sxs-lookup"><span data-stu-id="26126-145">Now resize hello filesystem with `resize2fs`:</span></span>

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. <span data-ttu-id="26126-146">Toohello partycji hello instalacji konieczne lokalizacji, takich jak `/datadrive`:</span><span class="sxs-lookup"><span data-stu-id="26126-146">Mount hello partition toohello desired location, such as `/datadrive`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. <span data-ttu-id="26126-147">Zmieniono rozmiar dysku systemu operacyjnego hello tooverify, użyj `df -h`.</span><span class="sxs-lookup"><span data-stu-id="26126-147">tooverify hello OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="26126-148">następujące przykładowe dane wyjściowe Hello pokazuje hello dysk danych, */dev/sdc1*, jest teraz 200 GB:</span><span class="sxs-lookup"><span data-stu-id="26126-148">hello following example output shows hello data drive, */dev/sdc1*, is now 200 GB:</span></span>

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a><span data-ttu-id="26126-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="26126-149">Next steps</span></span>
<span data-ttu-id="26126-150">Jeśli potrzebujesz dodatkowego magazynu, możesz również [dodać tooa dysków danych maszyny Wirtualnej systemu Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="26126-150">If you need additional storage, you also [add data disks tooa Linux VM](add-disk.md).</span></span> <span data-ttu-id="26126-151">Aby uzyskać więcej informacji o szyfrowaniu dysków, zobacz [szyfrowania dysków na Maszynę wirtualną systemu Linux przy użyciu hello Azure CLI](encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="26126-151">For more information about disk encryption, see [Encrypt disks on a Linux VM using hello Azure CLI](encrypt-disks.md).</span></span>
