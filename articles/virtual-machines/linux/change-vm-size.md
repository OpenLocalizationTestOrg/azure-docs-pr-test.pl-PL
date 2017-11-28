---
title: "tooresize aaaHow Maszynę wirtualną systemu Linux z hello Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Jak tooscale zapasowych lub Zmniejsz maszyny wirtualnej systemu Linux, zmieniając hello rozmiar maszyny Wirtualnej."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: e163f878-b919-45c5-9f5a-75a64f3b14a0
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2017
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e8fba485b5bcc7824f546de5cf3df77624a28008
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a><span data-ttu-id="af52f-103">Zmień rozmiar maszyny wirtualnej systemu Linux przy użyciu interfejsu wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="af52f-103">Resize a Linux virtual machine using CLI 2.0</span></span>

<span data-ttu-id="af52f-104">Po udostępnić maszynę wirtualną (VM), można skalować hello maszyny Wirtualnej w górę lub w dół, zmieniając hello [rozmiar maszyny Wirtualnej][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="af52f-104">After you provision a virtual machine (VM), you can scale hello VM up or down by changing hello [VM size][vm-sizes].</span></span> <span data-ttu-id="af52f-105">W niektórych przypadkach należy najpierw cofnąć hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="af52f-105">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="af52f-106">W razie potrzeby hello rozmiar nie jest dostępny na hello sprzętu klastra, który jest hostem hello maszyny Wirtualnej należy hello toodeallocate maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="af52f-106">You need toodeallocate hello VM if hello desired size is not available on hello hardware cluster that is hosting hello VM.</span></span> <span data-ttu-id="af52f-107">Ten artykuł zawiera szczegóły dotyczące sposobu tooresize a Linux VM z hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="af52f-107">This article details how tooresize a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="af52f-108">Można również wykonać te kroki hello [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="af52f-108">You can also perform these steps with hello [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="resize-a-vm"></a><span data-ttu-id="af52f-109">Zmienianie rozmiaru maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="af52f-109">Resize a VM</span></span>
<span data-ttu-id="af52f-110">tooresize maszyny Wirtualnej, należy hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="af52f-110">tooresize a VM, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

1. <span data-ttu-id="af52f-111">Wyświetl listę hello maszyny wirtualnej dostępne rozmiary na powitania sprzętu klastra, gdzie jest hostowana hello maszyny Wirtualnej z [az maszyny wirtualnej-vm — zmiany rozmiaru — opcje listy](/cli/azure/vm#list-vm-resize-options).</span><span class="sxs-lookup"><span data-stu-id="af52f-111">View hello list of available VM sizes on hello hardware cluster where hello VM is hosted with [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span></span> <span data-ttu-id="af52f-112">Witaj poniższy przykład zawiera listę rozmiarów maszyn wirtualnych dla maszyny Wirtualnej o nazwie hello `myVM` w grupie zasobów hello `myResourceGroup` regionu:</span><span class="sxs-lookup"><span data-stu-id="af52f-112">hello following example lists VM sizes for hello VM named `myVM` in hello resource group `myResourceGroup` region:</span></span>
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. <span data-ttu-id="af52f-113">W razie potrzeby hello znajduje się rozmiar maszyny Wirtualnej, należy zmienić rozmiar hello maszyny Wirtualnej z [Zmień rozmiar maszyny wirtualnej az](/cli/azure/vm#resize).</span><span class="sxs-lookup"><span data-stu-id="af52f-113">If hello desired VM size is listed, resize hello VM with [az vm resize](/cli/azure/vm#resize).</span></span> <span data-ttu-id="af52f-114">powitania po zmienia rozmiar przykład Witaj maszyny Wirtualnej o nazwie `myVM` toohello `Standard_DS3_v2` rozmiar:</span><span class="sxs-lookup"><span data-stu-id="af52f-114">hello following example resizes hello VM named `myVM` toohello `Standard_DS3_v2` size:</span></span>
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    <span data-ttu-id="af52f-115">Witaj maszyny Wirtualnej zostanie uruchomiony ponownie w trakcie tego procesu.</span><span class="sxs-lookup"><span data-stu-id="af52f-115">hello VM restarts during this process.</span></span> <span data-ttu-id="af52f-116">Po ponownym uruchomieniu hello są mapowane ponownie z istniejącego systemu operacyjnego i dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="af52f-116">After hello restart, your existing OS and data disks are remapped.</span></span> <span data-ttu-id="af52f-117">Elementy na dysku tymczasowym hello zostaną utracone.</span><span class="sxs-lookup"><span data-stu-id="af52f-117">Anything on hello temporary disk is lost.</span></span>

3. <span data-ttu-id="af52f-118">W razie potrzeby hello rozmiar maszyny Wirtualnej nie ma na liście należy toofirst deallocate hello maszyny Wirtualnej z [deallocate wirtualna az](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="af52f-118">If hello desired VM size is not listed, you need toofirst deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="af52f-119">Ten proces umożliwia hello toothen maszyny Wirtualnej jest dostępny rozmiar tooany po zmianie rozmiaru, który hello obsługuje region, a następnie uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="af52f-119">This process allows hello VM toothen be resized tooany size available that hello region supports and then started.</span></span> <span data-ttu-id="af52f-120">Witaj następujące kroki cofnięcie przydziału, Zmień rozmiar, a następnie uruchom hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="af52f-120">hello following steps deallocate, resize, and then start hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="af52f-121">Cofanie przydziału hello wirtualna zwalnia również dynamiczne adresy IP przypisane toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="af52f-121">Deallocating hello VM also releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="af52f-122">nie dotyczy Hello systemu operacyjnego i dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="af52f-122">hello OS and data disks are not affected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af52f-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="af52f-123">Next steps</span></span>
<span data-ttu-id="af52f-124">Dodatkowe możliwości skalowania uruchamianie wielu wystąpień maszyny Wirtualnej i skalowanie w poziomie. Aby uzyskać więcej informacji, zobacz [automatycznie skalować w zestawie skalowania maszyn wirtualnych systemu Linux maszyny][scale-set].</span><span class="sxs-lookup"><span data-stu-id="af52f-124">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
