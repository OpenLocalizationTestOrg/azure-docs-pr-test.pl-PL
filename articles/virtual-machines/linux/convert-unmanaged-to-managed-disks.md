---
title: "aaaConvert maszyny wirtualnej systemu Linux na platformie Azure z niezarządzanych dyski dysków toomanaged - dysków zarządzanych Azure | Dokumentacja firmy Microsoft"
description: "Jak dyski tooconvert Maszynę wirtualną systemu Linux z toomanaged niezarządzane dysków przy użyciu interfejsu wiersza polecenia Azure w wersji 2.0 w modelu wdrażania usługi Resource Manager hello"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 1b94da11deab46f344e28ab4491cf220506b6347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a><span data-ttu-id="43fbb-103">Konwertuj maszyny wirtualnej systemu Linux z dysków toomanaged niezarządzane dysków</span><span class="sxs-lookup"><span data-stu-id="43fbb-103">Convert a Linux virtual machine from unmanaged disks toomanaged disks</span></span>

<span data-ttu-id="43fbb-104">Jeśli masz istniejące maszyn wirtualnych systemu Linux (VM) korzystające z niezarządzanego dysków, można konwertować dyski toouse zarządzanych maszyn wirtualnych hello za pośrednictwem hello [dysków zarządzanych Azure](../windows/managed-disks-overview.md) usługi.</span><span class="sxs-lookup"><span data-stu-id="43fbb-104">If you have existing Linux virtual machines (VMs) that use unmanaged disks, you can convert hello VMs toouse managed disks through hello [Azure Managed Disks](../windows/managed-disks-overview.md) service.</span></span> <span data-ttu-id="43fbb-105">Ten proces konwersji dyskach hello systemu operacyjnego i wszystkich dysków dołączonych danych.</span><span class="sxs-lookup"><span data-stu-id="43fbb-105">This process converts both hello OS disk and any attached data disks.</span></span>

<span data-ttu-id="43fbb-106">W tym artykule opisano, jak tooconvert maszyn wirtualnych przy użyciu hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="43fbb-106">This article shows you how tooconvert VMs by using hello Azure CLI.</span></span> <span data-ttu-id="43fbb-107">Jeśli konieczne tooinstall lub uaktualnić go, zobacz [zainstalować Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="43fbb-107">If you need tooinstall or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="43fbb-108">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="43fbb-108">Before you begin</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a><span data-ttu-id="43fbb-109">Konwertuj maszyn wirtualnych z jednego wystąpienia</span><span class="sxs-lookup"><span data-stu-id="43fbb-109">Convert single-instance VMs</span></span>
<span data-ttu-id="43fbb-110">W tej sekcji omówiono sposób tooconvert jednym wystąpieniu maszyny wirtualne platformy Azure z niezarządzanych dyski toomanaged dyski.</span><span class="sxs-lookup"><span data-stu-id="43fbb-110">This section covers how tooconvert single-instance Azure VMs from unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="43fbb-111">(W przypadku maszyn wirtualnych w zestawie dostępności, zobacz następną sekcję hello). Można użyć tego procesu tooconvert hello maszyny wirtualne z dysków toopremium zarządzane dysków w warstwie premium (SSD) niezarządzanych lub standard (HDD) niezarządzanych dysków toostandard zarządzanych dysków.</span><span class="sxs-lookup"><span data-stu-id="43fbb-111">(If your VMs are in an availability set, see hello next section.) You can use this process tooconvert hello VMs from premium (SSD) unmanaged disks toopremium managed disks, or from standard (HDD) unmanaged disks toostandard managed disks.</span></span>

1. <span data-ttu-id="43fbb-112">Cofnięcie przydziału hello maszyny Wirtualnej za pomocą [deallocate wirtualna az](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="43fbb-112">Deallocate hello VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="43fbb-113">Witaj poniższy przykład cofa alokację hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="43fbb-113">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. <span data-ttu-id="43fbb-114">Skonwertuj dyski toomanaged wirtualna hello przy użyciu [konwersji maszyny wirtualnej az](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="43fbb-114">Convert hello VM toomanaged disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="43fbb-115">Hello następującego procesu konwertuje hello maszyny Wirtualnej o nazwie `myVM`, w tym dysku hello systemu operacyjnego i dysków z danymi:</span><span class="sxs-lookup"><span data-stu-id="43fbb-115">hello following process converts hello VM named `myVM`, including hello OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="43fbb-116">Rozpocznij hello maszyny Wirtualnej po hello konwersji toomanaged dysków za pomocą [uruchomienia maszyny wirtualnej az](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="43fbb-116">Start hello VM after hello conversion toomanaged disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="43fbb-117">Po uruchomieniu przykład Hello hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="43fbb-117">hello following example starts hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="43fbb-118">Konwertuj maszyn wirtualnych w zestawie dostępności</span><span class="sxs-lookup"><span data-stu-id="43fbb-118">Convert VMs in an availability set</span></span>

<span data-ttu-id="43fbb-119">Hello maszyn wirtualnych, które mają tooconvert toomanaged dyski znajdują się w zestawie dostępności, należy najpierw tooconvert hello dostępność zestawu tooa zarządzanego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="43fbb-119">If hello VMs that you want tooconvert toomanaged disks are in an availability set, you first need tooconvert hello availability set tooa managed availability set.</span></span>

<span data-ttu-id="43fbb-120">Wszystkie maszyny wirtualne w zestawie dostępności hello musi przydzielenia przed dokonaniem konwersji hello zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="43fbb-120">All VMs in hello availability set must be deallocated before you convert hello availability set.</span></span> <span data-ttu-id="43fbb-121">Wszystkie dyski toomanaged maszyn wirtualnych po udostępnieniu hello ustawić siebie tooconvert plan został przekonwertowany tooa zarządzanego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="43fbb-121">Plan tooconvert all VMs toomanaged disks after hello availability set itself has been converted tooa managed availability set.</span></span> <span data-ttu-id="43fbb-122">Następnie uruchom wszystkie maszyny wirtualne hello i kontynuowania działania jako standardowa.</span><span class="sxs-lookup"><span data-stu-id="43fbb-122">Then, start all hello VMs and continue operating as normal.</span></span>

1. <span data-ttu-id="43fbb-123">Wyświetl listę wszystkich maszyn wirtualnych w zestawie przy użyciu dostępności [listy zestawu dostępności maszyny wirtualnej az](/cli/azure/vm/availability-set#list).</span><span class="sxs-lookup"><span data-stu-id="43fbb-123">List all VMs in an availability set by using [az vm availability-set list](/cli/azure/vm/availability-set#list).</span></span> <span data-ttu-id="43fbb-124">Witaj poniższy przykład zawiera listę wszystkich maszyn wirtualnych w zestawie o nazwie dostępności hello `myAvailabilitySet` hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="43fbb-124">hello following example lists all VMs in hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. <span data-ttu-id="43fbb-125">Cofnięcie przydziału wszystkich hello maszyn wirtualnych za pomocą [deallocate wirtualna az](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="43fbb-125">Deallocate all hello VMs by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="43fbb-126">Witaj poniższy przykład cofa alokację hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="43fbb-126">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="43fbb-127">Konwertuj dostępności hello skonfigurowane za pomocą [przekonwertować zestawu dostępności maszyny wirtualnej az](/cli/azure/vm/availability-set#convert).</span><span class="sxs-lookup"><span data-stu-id="43fbb-127">Convert hello availability set by using [az vm availability-set convert](/cli/azure/vm/availability-set#convert).</span></span> <span data-ttu-id="43fbb-128">Witaj poniższy przykład konwertuje zestaw o nazwie dostępności hello `myAvailabilitySet` hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="43fbb-128">hello following example converts hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. <span data-ttu-id="43fbb-129">Konwertuj wszystkie dyski toomanaged maszyn wirtualnych hello przy użyciu [konwersji maszyny wirtualnej az](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="43fbb-129">Convert all hello VMs toomanaged disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="43fbb-130">Hello następującego procesu konwertuje hello maszyny Wirtualnej o nazwie `myVM`, w tym dysku hello systemu operacyjnego i dysków z danymi:</span><span class="sxs-lookup"><span data-stu-id="43fbb-130">hello following process converts hello VM named `myVM`, including hello OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. <span data-ttu-id="43fbb-131">Uruchomienie wszystkich maszyn wirtualnych powitania po hello konwersji toomanaged dysków za pomocą [uruchomienia maszyny wirtualnej az](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="43fbb-131">Start all hello VMs after hello conversion toomanaged disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="43fbb-132">Po uruchomieniu przykład Hello hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="43fbb-132">hello following example starts hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="43fbb-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="43fbb-133">Next steps</span></span>
<span data-ttu-id="43fbb-134">Aby uzyskać więcej informacji na temat opcji magazynu, zobacz [omówienie dysków zarządzanych Azure](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="43fbb-134">For more information about storage options, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>
