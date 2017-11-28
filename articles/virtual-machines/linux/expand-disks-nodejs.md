---
title: "Zwiększ rozmiar dysku systemu operacyjnego na maszynie Wirtualnej systemu Linux z interfejsu wiersza polecenia platformy Azure w wersji 1.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak rozszerzyć wirtualny dysk systemu operacyjnego (OS) na maszynie Wirtualnej systemu Linux przy użyciu 1.0 interfejsu wiersza polecenia platformy Azure i modelu wdrażania usługi Resource Manager"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0aedcd70b54c2ed47ec327ccf0529a48351353c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="expand-os-disk-on-a-linux-vm-using-the-azure-cli-with-the-azure-cli-10"></a><span data-ttu-id="0b365-103">Zwiększ rozmiar dysku systemu operacyjnego na maszynie Wirtualnej systemu Linux przy użyciu wiersza polecenia platformy Azure z interfejsu wiersza polecenia platformy Azure w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="0b365-103">Expand OS disk on a Linux VM using the Azure CLI with the Azure CLI 1.0</span></span>
<span data-ttu-id="0b365-104">Domyślny rozmiar wirtualnego dysku twardego systemu operacyjnego (OS) jest zwykle 30 GB na maszynie wirtualnej systemu Linux (VM) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0b365-104">The default virtual hard disk size for the operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="0b365-105">Możesz [Dodaj dyski danych](add-disk.md) zapewnienie dodatkowego miejsca, ale mogą też chcieć Zwiększ rozmiar dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="0b365-105">You can [add data disks](add-disk.md) to provide for additional storage space, but you may also wish to expand the OS disk.</span></span> <span data-ttu-id="0b365-106">Ten artykuł zawiera szczegóły dotyczące sposobu rozszerzania dysku systemu operacyjnego dla maszyny Wirtualnej systemu Linux przy użyciu niezarządzanych dysków z interfejsu wiersza polecenia platformy Azure w wersji 1.0.</span><span class="sxs-lookup"><span data-stu-id="0b365-106">This article details how to expand the OS disk for a Linux VM using unmanaged disks with the Azure CLI 1.0.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="0b365-107">Wersje interfejsu wiersza polecenia umożliwiające wykonanie zadania</span><span class="sxs-lookup"><span data-stu-id="0b365-107">CLI versions to complete the task</span></span>
<span data-ttu-id="0b365-108">Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="0b365-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="0b365-109">[Azure CLI 1.0](#prerequisites) — nasze interfejsu wiersza polecenia dla klasycznego i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="0b365-109">[Azure CLI 1.0](#prerequisites) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="0b365-110">[Interfejs wiersza polecenia platformy Azure w wersji 2.0](expand-disks.md) — nasz interfejs wiersza polecenia nowej generacji dla modelu wdrażania na potrzeby zarządzania zasobami</span><span class="sxs-lookup"><span data-stu-id="0b365-110">[Azure CLI 2.0](expand-disks.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b365-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0b365-111">Prerequisites</span></span>
<span data-ttu-id="0b365-112">Należy [najnowsze Azure CLI 1.0](../../cli-install-nodejs.md) zainstalowane i zarejestrowane celu [konta Azure](https://azure.microsoft.com/pricing/free-trial/) przy użyciu tryb usługi Resource Manager w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="0b365-112">You need the [latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in to an [Azure account](https://azure.microsoft.com/pricing/free-trial/) using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="0b365-113">W poniższych przykładach Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="0b365-113">In the following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="0b365-114">Przykład nazwy parametru zawierają *myResourceGroup* i *myVM*.</span><span class="sxs-lookup"><span data-stu-id="0b365-114">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

## <a name="expand-os-disk"></a><span data-ttu-id="0b365-115">Rozszerzanie dysku systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="0b365-115">Expand OS disk</span></span>

1. <span data-ttu-id="0b365-116">Nie można wykonać operacji na wirtualnych dyskach twardych z uruchomionych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="0b365-116">Operations on virtual hard disks cannot be performed with the VM running.</span></span> <span data-ttu-id="0b365-117">W poniższym przykładzie zatrzymuje i cofa alokację maszyny Wirtualnej o nazwie *myVM* w grupie zasobów o nazwie *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="0b365-117">The following example stops and deallocates the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="0b365-118">`azure vm stop`zwalnia zasoby obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="0b365-118">`azure vm stop` does not release the compute resources.</span></span> <span data-ttu-id="0b365-119">Aby zwolnić zasoby obliczeniowe, użyj `azure vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="0b365-119">To release compute resources, use `azure vm deallocate`.</span></span> <span data-ttu-id="0b365-120">Aby zwiększyć rozmiaru wirtualnego dysku twardego, można cofnąć przydziału maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0b365-120">The VM must be deallocated to expand the virtual hard disk.</span></span>

2. <span data-ttu-id="0b365-121">Aktualizacja rozmiaru niezarządzane użycie dysku systemu operacyjnego `azure vm set` polecenia.</span><span class="sxs-lookup"><span data-stu-id="0b365-121">Update the size of the unmanaged OS disk using the `azure vm set` command.</span></span> <span data-ttu-id="0b365-122">Poniższy przykład aktualizuje maszyny Wirtualnej o nazwie *myVM* w grupie zasobów o nazwie *myResourceGroup* jako *50* GB:</span><span class="sxs-lookup"><span data-stu-id="0b365-122">The following example updates the VM named *myVM* in the resource group named *myResourceGroup* to be *50* GB:</span></span>

    ```azurecli
    azure vm set \
        --resource-group myResourceGroup \
        --name myVM \
        --new-os-disk-size 50
    ```

3. <span data-ttu-id="0b365-123">Uruchom maszyny Wirtualnej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="0b365-123">Start your VM as follows:</span></span>

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="0b365-124">SSH do maszyny Wirtualnej przy użyciu odpowiednich poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="0b365-124">SSH to your VM with the appropriate credentials.</span></span> <span data-ttu-id="0b365-125">Aby sprawdzić, zmiany rozmiaru dysku systemu operacyjnego, użyj `df -h`.</span><span class="sxs-lookup"><span data-stu-id="0b365-125">To verify the OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="0b365-126">Partycja podstawowa zawiera następujące przykładowe dane wyjściowe (*/dev/sda1*) jest teraz 50 GB:</span><span class="sxs-lookup"><span data-stu-id="0b365-126">The following example output shows the primary partition (*/dev/sda1*) is now 50 GB:</span></span>

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a><span data-ttu-id="0b365-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0b365-127">Next steps</span></span>
<span data-ttu-id="0b365-128">Jeśli potrzebujesz dodatkowego magazynu, możesz również [Dodaj dyski danych do maszyny Wirtualnej systemu Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="0b365-128">If you need additional storage, you also [add data disks to a Linux VM](add-disk.md).</span></span> <span data-ttu-id="0b365-129">Aby uzyskać więcej informacji o szyfrowaniu dysków, zobacz [szyfrowania dysków na Maszynę wirtualną systemu Linux przy użyciu interfejsu wiersza polecenia Azure](encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="0b365-129">For more information about disk encryption, see [Encrypt disks on a Linux VM using the Azure CLI](encrypt-disks.md).</span></span>
