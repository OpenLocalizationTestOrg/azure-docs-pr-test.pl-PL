---
title: "Jak zmienić rozmiar maszyny Wirtualnej systemu Linux, z interfejsu wiersza polecenia platformy Azure w wersji 1.0 | Dokumentacja firmy Microsoft"
description: "Jak skalowanie w górę i skalowania maszynę wirtualną systemu Linux przez zmianę rozmiaru maszyny Wirtualnej."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2016
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 72f5a3cd6463befd5108040ed166984281bfc5f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="resize-a-linux-vm-with-azure-cli-10"></a><span data-ttu-id="147d9-103">Zmień rozmiar maszyny Wirtualnej systemu Linux z interfejsu wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="147d9-103">Resize a Linux VM with Azure CLI 1.0</span></span>

## <a name="overview"></a><span data-ttu-id="147d9-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="147d9-104">Overview</span></span>

<span data-ttu-id="147d9-105">Po udostępnić maszynę wirtualną (VM), można skalować maszyny Wirtualnej w górę lub w dół, zmieniając [rozmiar maszyny Wirtualnej][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="147d9-105">After you provision a virtual machine (VM), you can scale the VM up or down by changing the [VM size][vm-sizes].</span></span> <span data-ttu-id="147d9-106">W niektórych przypadkach należy najpierw cofnąć maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="147d9-106">In some cases, you must deallocate the VM first.</span></span> <span data-ttu-id="147d9-107">Może to nastąpić, jeśli nowy rozmiar jest niedostępny w klastrze sprzętu, który jest hostem maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="147d9-107">This can happen if the new size is not available on the hardware cluster that is hosting the VM.</span></span>

<span data-ttu-id="147d9-108">W tym artykule przedstawiono sposób zmiany rozmiaru maszyny Wirtualnej systemu Linux przy użyciu [interfejsu wiersza polecenia Azure][azure-cli].</span><span class="sxs-lookup"><span data-stu-id="147d9-108">This article shows how to resize a Linux VM using the [Azure CLI][azure-cli].</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="147d9-109">Wersje interfejsu wiersza polecenia umożliwiające wykonanie zadania</span><span class="sxs-lookup"><span data-stu-id="147d9-109">CLI versions to complete the task</span></span>
<span data-ttu-id="147d9-110">Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="147d9-110">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="147d9-111">[Azure CLI 1.0](#resize-a-linux-vm) — nasze interfejsu wiersza polecenia dla klasycznego i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="147d9-111">[Azure CLI 1.0](#resize-a-linux-vm) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="147d9-112">[Interfejs wiersza polecenia platformy Azure w wersji 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) — nasz interfejs wiersza polecenia nowej generacji dla modelu wdrażania na potrzeby zarządzania zasobami</span><span class="sxs-lookup"><span data-stu-id="147d9-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="resize-a-linux-vm"></a><span data-ttu-id="147d9-113">Zmień rozmiar maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="147d9-113">Resize a Linux VM</span></span>
<span data-ttu-id="147d9-114">Aby zmienić rozmiar maszyny Wirtualnej, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="147d9-114">To resize a VM, perform the following steps.</span></span>

1. <span data-ttu-id="147d9-115">Uruchom następujące polecenie, interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="147d9-115">Run the following CLI command.</span></span> <span data-ttu-id="147d9-116">To polecenie wyświetla listę rozmiarów maszyn wirtualnych, które są dostępne w klastrze sprzętu, gdzie jest hostowana maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="147d9-116">This command lists the VM sizes that are available on the hardware cluster where the VM is hosted.</span></span>
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. <span data-ttu-id="147d9-117">Jeśli na liście jest wymagany rozmiar, uruchom następujące polecenie, aby zmienić rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="147d9-117">If the desired size is listed, run the following command to resize the VM.</span></span>
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    <span data-ttu-id="147d9-118">Maszyna wirtualna zostanie ponownie uruchomiona w trakcie tego procesu.</span><span class="sxs-lookup"><span data-stu-id="147d9-118">The VM will restart during this process.</span></span> <span data-ttu-id="147d9-119">Po uruchomieniu z istniejącego systemu operacyjnego i dysków z danymi będzie można ponownie zamapować.</span><span class="sxs-lookup"><span data-stu-id="147d9-119">After the restart, your existing OS and data disks will be remapped.</span></span> <span data-ttu-id="147d9-120">Elementy na dysku tymczasowym zostaną utracone.</span><span class="sxs-lookup"><span data-stu-id="147d9-120">Anything on the temporary disk will be lost.</span></span>
   
    <span data-ttu-id="147d9-121">Użyj `--enable-boot-diagnostics` powoduje włączenie [diagnostyki rozruchu][boot-diagnostics], aby rejestrować błędy dotyczące uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="147d9-121">Use the `--enable-boot-diagnostics` option enables [boot diagnostics][boot-diagnostics], to log any errors related to startup.</span></span>
3. <span data-ttu-id="147d9-122">W przeciwnym razie Jeśli żądany rozmiar nie jest wyświetlana, uruchom następujące polecenia można cofnąć alokacji maszyny Wirtualnej, rozmiar i ponownie uruchom maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="147d9-122">Otherwise, if the desired size is not listed, run the following commands to deallocate the VM, resize it, and then restart the VM.</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="147d9-123">Cofanie przydziału maszyny Wirtualnej zwalnia również dynamiczne adresy IP przypisane do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="147d9-123">Deallocating the VM also releases any dynamic IP addresses assigned to the VM.</span></span> <span data-ttu-id="147d9-124">Nie dotyczy systemu operacyjnego i dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="147d9-124">The OS and data disks are not affected.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="147d9-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="147d9-125">Next steps</span></span>
<span data-ttu-id="147d9-126">Dodatkowe możliwości skalowania uruchamianie wielu wystąpień maszyny Wirtualnej i skalowanie w poziomie.</span><span class="sxs-lookup"><span data-stu-id="147d9-126">For additional scalability, run multiple VM instances and scale out.</span></span> <span data-ttu-id="147d9-127">Aby uzyskać więcej informacji, zobacz [automatycznie skalować w zestawie skalowania maszyn wirtualnych systemu Linux maszyny][scale-set].</span><span class="sxs-lookup"><span data-stu-id="147d9-127">For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
