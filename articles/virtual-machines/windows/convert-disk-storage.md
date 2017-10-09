---
title: "aaaConvert Azure zarządzanego magazynu dysków z toopremium standardowe i na odwrót | Dokumentacja firmy Microsoft"
description: "Jak tooconvert Azure zarządzane dysków z toopremium standardowe i na odwrót, przy użyciu programu Azure PowerShell."
services: virtual-machines-windows
documentationcenter: 
author: ramankum
manager: kavithag
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ramankum
ms.openlocfilehash: 11f35cde216e91c0599d3619682686e8eb162fad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="c2b2e-103">Konwertuj Azure zarządzanego magazynu dysków z toopremium standardowe i na odwrót</span><span class="sxs-lookup"><span data-stu-id="c2b2e-103">Convert Azure managed disks storage from standard toopremium, and vice versa</span></span>

<span data-ttu-id="c2b2e-104">Zarządzane dysków oferuje dwie opcje magazynu: [Premium](../../storage/storage-premium-storage.md) (oparte na dysk SSD) i [standardowe](../../storage/storage-standard-storage.md) (oparte na dysk twardy).</span><span class="sxs-lookup"><span data-stu-id="c2b2e-104">Managed disks offers two storage options: [Premium](../../storage/storage-premium-storage.md) (SSD-based) and [Standard](../../storage/storage-standard-storage.md) (HDD-based).</span></span> <span data-ttu-id="c2b2e-105">Pozwala ona tooeasily przełączanie między Witaj dwie opcje z minimalnym czasem przestojów na podstawie Twoich potrzeb wydajności.</span><span class="sxs-lookup"><span data-stu-id="c2b2e-105">It allows you tooeasily switch between hello two options with minimal downtime based on your performance needs.</span></span> <span data-ttu-id="c2b2e-106">Ta funkcja nie jest dostępna dla niezarządzanego dysków.</span><span class="sxs-lookup"><span data-stu-id="c2b2e-106">This capability is not available for unmanaged disks.</span></span> <span data-ttu-id="c2b2e-107">Ale możesz z łatwością [skonwertuj dyski toomanaged](convert-unmanaged-to-managed-disks.md) tooeasily przełączanie między Witaj dwie opcje.</span><span class="sxs-lookup"><span data-stu-id="c2b2e-107">But you can easily [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) tooeasily switch between hello two options.</span></span>

<span data-ttu-id="c2b2e-108">W tym artykule opisano sposób tooconvert zarządzania dysków z toopremium standardowe i na odwrót przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2b2e-108">This article shows you how tooconvert managed disks from standard toopremium, and vice versa by using Azure PowerShell.</span></span> <span data-ttu-id="c2b2e-109">Jeśli konieczne tooinstall lub uaktualnić go, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c2b2e-109">If you need tooinstall or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c2b2e-110">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="c2b2e-110">Before you begin</span></span>

* <span data-ttu-id="c2b2e-111">Hello konwersja wymaga ponownego uruchomienia hello maszyny Wirtualnej, więc planowanie migracji hello magazynu dysków w istniejącym oknie obsługi.</span><span class="sxs-lookup"><span data-stu-id="c2b2e-111">hello conversion requires a restart of hello VM, so schedule hello migration of your disks storage during a pre-existing maintenance window.</span></span> 
* <span data-ttu-id="c2b2e-112">Jeśli używane są niezarządzane dysków, najpierw [skonwertuj dyski toomanaged](convert-unmanaged-to-managed-disks.md) toouse tooswitch tego artykułu między Witaj dwie opcje magazynu.</span><span class="sxs-lookup"><span data-stu-id="c2b2e-112">If you are using unmanaged disks, first [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) toouse this article tooswitch between hello two storage options.</span></span> 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="c2b2e-113">Konwertuj hello wszystkie zarządzane dyski maszyny wirtualnej z toopremium standardowe i na odwrót</span><span class="sxs-lookup"><span data-stu-id="c2b2e-113">Convert all hello managed disks of a VM from standard toopremium, and vice versa</span></span>

<span data-ttu-id="c2b2e-114">W hello poniższy przykład, zostanie przedstawiony sposób tooswitch hello wszystkie dyski maszyny Wirtualnej z magazynu standardowego toopremium.</span><span class="sxs-lookup"><span data-stu-id="c2b2e-114">In hello following example, we show how tooswitch all hello disks of a VM from standard toopremium storage.</span></span> <span data-ttu-id="c2b2e-115">toouse premium zarządzane dyski, należy użyć maszyny Wirtualnej [rozmiar maszyny Wirtualnej](sizes.md) obsługującym magazyn w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="c2b2e-115">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="c2b2e-116">W tym przykładzie również zmienia rozmiar tooa, który obsługuje magazyn w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="c2b2e-116">This example also switches tooa size that supports premium storage.</span></span>

```powershell
# Name of hello resource group that contains hello VM
$rgName = 'yourResourceGroup'

# Name of hello your virtual machine
$vmName = 'yourVM'

# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'

# Premium capable size
# Required only if converting storage from standard toopremium
$size = 'Standard_DS2_v2'
$vm = Get-AzureRmVM -Name $vmName -resourceGroupName $rgName

# Stop and deallocate hello VM before changing hello size
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force

# Change hello VM size tooa size that supports premium storage
# Skip this step if converting storage from premium toostandard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Get all disks in hello resource group of hello VM
$vmDisks = Get-AzureRmDisk -ResourceGroupName $rgName 

# For disks that belong toohello selected VM, convert toopremium storage
foreach ($disk in $vmDisks)
{
    if ($disk.OwnerId -eq $vm.Id)
    {
        $diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
        Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
        -DiskName $disk.Name
    }
}

Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="c2b2e-117">Konwertuj dysk zarządzanego z toopremium standardowe i na odwrót</span><span class="sxs-lookup"><span data-stu-id="c2b2e-117">Convert a managed disk from standard toopremium, and vice versa</span></span>

<span data-ttu-id="c2b2e-118">Dla obciążenia i testowania możesz toohave kombinację dysków warstwy standardowa i premium tooreduce koszt.</span><span class="sxs-lookup"><span data-stu-id="c2b2e-118">For your dev/test workload, you may want toohave mixture of standard and premium disks tooreduce your cost.</span></span> <span data-ttu-id="c2b2e-119">Można wykonać je przez uaktualnienie magazynu toopremium tylko dyski hello, które wymagają lepszą wydajność.</span><span class="sxs-lookup"><span data-stu-id="c2b2e-119">You can accomplish it by upgrading toopremium storage, only hello disks that require better performance.</span></span> <span data-ttu-id="c2b2e-120">W hello poniższy przykład, zostanie przedstawiony sposób tooswitch jednego dysku maszyny wirtualnej z magazynu standardowego toopremium i na odwrót.</span><span class="sxs-lookup"><span data-stu-id="c2b2e-120">In hello following example, we show how tooswitch a single disk of a VM from standard toopremium storage, and vice versa.</span></span> <span data-ttu-id="c2b2e-121">toouse premium zarządzane dyski, należy użyć maszyny Wirtualnej [rozmiar maszyny Wirtualnej](sizes.md) obsługującym magazyn w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="c2b2e-121">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="c2b2e-122">W tym przykładzie również zmienia rozmiar tooa, który obsługuje magazyn w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="c2b2e-122">This example also switches tooa size that supports premium storage.</span></span>

```powershell

$diskName = 'yourDiskName'
# resource group that contains hello managed disk
$rgName = 'yourResourceGroupName'
# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'
# Premium capable size 
$size = 'Standard_DS2_v2'

$disk = Get-AzureRmDisk -DiskName $diskName -ResourceGroupName $rgName

# Get hello ARM resource tooget name and resource group of hello VM
$vmResource = Get-AzureRmResource -ResourceId $disk.OwnerId
$vm = Get-AzureRmVM $vmResource.ResourceGroupName -Name $vmResource.ResourceName 

# Stop and deallocate hello VM before changing hello storage type
Stop-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name -Force

# Change hello VM size tooa size that supports premium storage
# Skip this step if converting storage from premium toostandard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Update hello storage type
$diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
-DiskName $disk.Name

Start-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name
```

## <a name="next-steps"></a><span data-ttu-id="c2b2e-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c2b2e-123">Next steps</span></span>

<span data-ttu-id="c2b2e-124">Podjąć tylko do odczytu kopię maszyny Wirtualnej za pomocą [migawki](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="c2b2e-124">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

