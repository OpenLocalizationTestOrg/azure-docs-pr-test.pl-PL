---
title: dysk aaaExpand systemu operacyjnego na maszynie Wirtualnej systemu Linux z hello Azure CLI 1.0 | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooexpand hello wirtualny dysk systemu operacyjnego (OS) na maszynie Wirtualnej systemu Linux przy użyciu hello Azure CLI 1.0 i modelu wdrażania usługi Resource Manager hello"
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
ms.openlocfilehash: 0db78c0b86b48b2c5358611e11bb0b7ad781a559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="expand-os-disk-on-a-linux-vm-using-hello-azure-cli-with-hello-azure-cli-10"></a><span data-ttu-id="ad3ff-103">Zwiększ rozmiar dysku systemu operacyjnego na maszynie Wirtualnej systemu Linux przy użyciu interfejsu wiersza polecenia Azure hello z hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="ad3ff-103">Expand OS disk on a Linux VM using hello Azure CLI with hello Azure CLI 1.0</span></span>
<span data-ttu-id="ad3ff-104">Witaj domyślny rozmiar wirtualnego dysku twardego systemu operacyjnego hello (systemu operacyjnego) jest zwykle 30 GB na maszynie wirtualnej systemu Linux (VM) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ad3ff-104">hello default virtual hard disk size for hello operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="ad3ff-105">Możesz [Dodaj dyski danych](add-disk.md) tooprovide dla dodatkowego miejsca, ale możesz również tooexpand dysku hello systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="ad3ff-105">You can [add data disks](add-disk.md) tooprovide for additional storage space, but you may also wish tooexpand hello OS disk.</span></span> <span data-ttu-id="ad3ff-106">W tym artykule szczegółowo sposób hello tooexpand systemu operacyjnego na dysku dla maszyny Wirtualnej systemu Linux przy użyciu niezarządzanych dysków z hello Azure CLI w wersji 1.0.</span><span class="sxs-lookup"><span data-stu-id="ad3ff-106">This article details how tooexpand hello OS disk for a Linux VM using unmanaged disks with hello Azure CLI 1.0.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="ad3ff-107">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="ad3ff-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="ad3ff-108">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="ad3ff-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="ad3ff-109">[Azure CLI 1.0](#prerequisites) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="ad3ff-109">[Azure CLI 1.0](#prerequisites) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="ad3ff-110">[Azure CLI 2.0](expand-disks.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="ad3ff-110">[Azure CLI 2.0](expand-disks.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad3ff-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ad3ff-111">Prerequisites</span></span>
<span data-ttu-id="ad3ff-112">Należy hello [najnowsze Azure CLI 1.0](../../cli-install-nodejs.md) zainstalowane i zarejestrowane w tooan [konta Azure](https://azure.microsoft.com/pricing/free-trial/) przy użyciu tryb usługi Resource Manager hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ad3ff-112">You need hello [latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in tooan [Azure account](https://azure.microsoft.com/pricing/free-trial/) using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="ad3ff-113">Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="ad3ff-113">In hello following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="ad3ff-114">Przykład nazwy parametru zawierają *myResourceGroup* i *myVM*.</span><span class="sxs-lookup"><span data-stu-id="ad3ff-114">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

## <a name="expand-os-disk"></a><span data-ttu-id="ad3ff-115">Rozszerzanie dysku systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="ad3ff-115">Expand OS disk</span></span>

1. <span data-ttu-id="ad3ff-116">Nie można wykonać operacji na wirtualnych dyskach twardych z hello wirtualna uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="ad3ff-116">Operations on virtual hard disks cannot be performed with hello VM running.</span></span> <span data-ttu-id="ad3ff-117">Witaj poniższy przykład zatrzymuje i zwalnia hello maszyny Wirtualnej o nazwie *myVM* hello grupy zasobów o nazwie *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="ad3ff-117">hello following example stops and deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="ad3ff-118">`azure vm stop`zwalnia zasoby obliczeniowe hello.</span><span class="sxs-lookup"><span data-stu-id="ad3ff-118">`azure vm stop` does not release hello compute resources.</span></span> <span data-ttu-id="ad3ff-119">toorelease zasoby obliczeniowe, użyj `azure vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="ad3ff-119">toorelease compute resources, use `azure vm deallocate`.</span></span> <span data-ttu-id="ad3ff-120">Witaj maszyny Wirtualnej można cofnąć przydziału tooexpand hello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="ad3ff-120">hello VM must be deallocated tooexpand hello virtual hard disk.</span></span>

2. <span data-ttu-id="ad3ff-121">Zaktualizuj hello rozmiar dysku systemu operacyjnego hello niezarządzanych za pomocą hello `azure vm set` polecenia.</span><span class="sxs-lookup"><span data-stu-id="ad3ff-121">Update hello size of hello unmanaged OS disk using hello `azure vm set` command.</span></span> <span data-ttu-id="ad3ff-122">Po aktualizacji przykład Hello hello maszyny Wirtualnej o nazwie *myVM* hello grupy zasobów o nazwie *myResourceGroup* toobe *50* GB:</span><span class="sxs-lookup"><span data-stu-id="ad3ff-122">hello following example updates hello VM named *myVM* in hello resource group named *myResourceGroup* toobe *50* GB:</span></span>

    ```azurecli
    azure vm set \
        --resource-group myResourceGroup \
        --name myVM \
        --new-os-disk-size 50
    ```

3. <span data-ttu-id="ad3ff-123">Uruchom maszyny Wirtualnej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ad3ff-123">Start your VM as follows:</span></span>

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="ad3ff-124">Tooyour SSH maszyny Wirtualnej z hello odpowiednie poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="ad3ff-124">SSH tooyour VM with hello appropriate credentials.</span></span> <span data-ttu-id="ad3ff-125">Zmieniono rozmiar dysku systemu operacyjnego hello tooverify, użyj `df -h`.</span><span class="sxs-lookup"><span data-stu-id="ad3ff-125">tooverify hello OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="ad3ff-126">następujące przykładowe dane wyjściowe Hello pokazuje hello partycji podstawowej (*/dev/sda1*) jest teraz 50 GB:</span><span class="sxs-lookup"><span data-stu-id="ad3ff-126">hello following example output shows hello primary partition (*/dev/sda1*) is now 50 GB:</span></span>

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a><span data-ttu-id="ad3ff-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ad3ff-127">Next steps</span></span>
<span data-ttu-id="ad3ff-128">Jeśli potrzebujesz dodatkowego magazynu, możesz również [dodać tooa dysków danych maszyny Wirtualnej systemu Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="ad3ff-128">If you need additional storage, you also [add data disks tooa Linux VM](add-disk.md).</span></span> <span data-ttu-id="ad3ff-129">Aby uzyskać więcej informacji o szyfrowaniu dysków, zobacz [szyfrowania dysków na Maszynę wirtualną systemu Linux przy użyciu hello Azure CLI](encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="ad3ff-129">For more information about disk encryption, see [Encrypt disks on a Linux VM using hello Azure CLI](encrypt-disks.md).</span></span>
