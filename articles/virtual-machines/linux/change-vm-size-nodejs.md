---
title: "tooresize aaaHow Maszynę wirtualną systemu Linux z hello Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Jak tooscale zapasowych lub Zmniejsz maszyny wirtualnej systemu Linux, zmieniając hello rozmiar maszyny Wirtualnej."
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
ms.openlocfilehash: 43dd955dc2f2dd9d1b2da07ecbfbf2459bcaa4d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-vm-with-azure-cli-10"></a><span data-ttu-id="23126-103">Zmień rozmiar maszyny Wirtualnej systemu Linux z interfejsu wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="23126-103">Resize a Linux VM with Azure CLI 1.0</span></span>

## <a name="overview"></a><span data-ttu-id="23126-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="23126-104">Overview</span></span>

<span data-ttu-id="23126-105">Po udostępnić maszynę wirtualną (VM), można skalować hello maszyny Wirtualnej w górę lub w dół, zmieniając hello [rozmiar maszyny Wirtualnej][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="23126-105">After you provision a virtual machine (VM), you can scale hello VM up or down by changing hello [VM size][vm-sizes].</span></span> <span data-ttu-id="23126-106">W niektórych przypadkach należy najpierw cofnąć hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="23126-106">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="23126-107">Może to nastąpić, jeśli hello nowy rozmiar jest niedostępny na hello sprzętu klastra, który jest hostem hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="23126-107">This can happen if hello new size is not available on hello hardware cluster that is hosting hello VM.</span></span>

<span data-ttu-id="23126-108">W tym artykule przedstawiono sposób tooresize a maszyny Wirtualnej systemu Linux przy użyciu hello [interfejsu wiersza polecenia Azure][azure-cli].</span><span class="sxs-lookup"><span data-stu-id="23126-108">This article shows how tooresize a Linux VM using hello [Azure CLI][azure-cli].</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="23126-109">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="23126-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="23126-110">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="23126-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="23126-111">[Azure CLI 1.0](#resize-a-linux-vm) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="23126-111">[Azure CLI 1.0](#resize-a-linux-vm) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="23126-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="23126-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="resize-a-linux-vm"></a><span data-ttu-id="23126-113">Zmień rozmiar maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="23126-113">Resize a Linux VM</span></span>
<span data-ttu-id="23126-114">tooresize maszyny Wirtualnej, wykonaj hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="23126-114">tooresize a VM, perform hello following steps.</span></span>

1. <span data-ttu-id="23126-115">Uruchom następujące polecenia interfejsu wiersza polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="23126-115">Run hello following CLI command.</span></span> <span data-ttu-id="23126-116">To polecenie wyświetla hello rozmiarów maszyn wirtualnych, które są dostępne w klastrze sprzętu hello gdzie hello maszyny Wirtualnej jest hostowana.</span><span class="sxs-lookup"><span data-stu-id="23126-116">This command lists hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span>
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. <span data-ttu-id="23126-117">W razie potrzeby hello znajduje się rozmiar Uruchom hello następujące polecenia tooresize hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="23126-117">If hello desired size is listed, run hello following command tooresize hello VM.</span></span>
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    <span data-ttu-id="23126-118">Witaj maszyna wirtualna zostanie ponownie uruchomiona w trakcie tego procesu.</span><span class="sxs-lookup"><span data-stu-id="23126-118">hello VM will restart during this process.</span></span> <span data-ttu-id="23126-119">Po ponownym uruchomieniu hello z istniejącego systemu operacyjnego i dysków z danymi będzie można ponownie zamapować.</span><span class="sxs-lookup"><span data-stu-id="23126-119">After hello restart, your existing OS and data disks will be remapped.</span></span> <span data-ttu-id="23126-120">Elementy na dysku tymczasowym hello zostaną utracone.</span><span class="sxs-lookup"><span data-stu-id="23126-120">Anything on hello temporary disk will be lost.</span></span>
   
    <span data-ttu-id="23126-121">Użyj hello `--enable-boot-diagnostics` powoduje włączenie [diagnostyki rozruchu][boot-diagnostics], toolog żadnych toostartup powiązane błędy.</span><span class="sxs-lookup"><span data-stu-id="23126-121">Use hello `--enable-boot-diagnostics` option enables [boot diagnostics][boot-diagnostics], toolog any errors related toostartup.</span></span>
3. <span data-ttu-id="23126-122">W przeciwnym razie w razie potrzeby hello się, że nie ma rozmiar Uruchom hello następujące polecenia toodeallocate hello maszyny Wirtualnej, jej rozmiar, a następnie ponownie uruchom hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="23126-122">Otherwise, if hello desired size is not listed, run hello following commands toodeallocate hello VM, resize it, and then restart hello VM.</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="23126-123">Cofanie przydziału hello wirtualna zwalnia również dynamiczne adresy IP przypisane toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="23126-123">Deallocating hello VM also releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="23126-124">nie dotyczy Hello systemu operacyjnego i dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="23126-124">hello OS and data disks are not affected.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="23126-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="23126-125">Next steps</span></span>
<span data-ttu-id="23126-126">Dodatkowe możliwości skalowania uruchamianie wielu wystąpień maszyny Wirtualnej i skalowanie w poziomie. Aby uzyskać więcej informacji, zobacz [automatycznie skalować w zestawie skalowania maszyn wirtualnych systemu Linux maszyny][scale-set].</span><span class="sxs-lookup"><span data-stu-id="23126-126">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
