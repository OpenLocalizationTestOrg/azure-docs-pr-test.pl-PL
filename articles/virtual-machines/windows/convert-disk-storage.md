---
title: "Konwertuj Azure zarządzanego dyski magazynu ze standardu do premium i na odwrót | Dokumentacja firmy Microsoft"
description: "Jak przekonwertować Azure zarządzane dysków ze standardu do premium i odwrotnie, przy użyciu programu Azure PowerShell."
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
ms.openlocfilehash: 9e5c73ceb0ff7d9c18c9cf7128b69e40b9796874
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-to-premium-and-vice-versa"></a><span data-ttu-id="ad160-103">Konwertuj Azure zarządzanego dyski magazynu ze standardu do premium i na odwrót</span><span class="sxs-lookup"><span data-stu-id="ad160-103">Convert Azure managed disks storage from standard to premium, and vice versa</span></span>

<span data-ttu-id="ad160-104">Zarządzane dysków oferuje dwie opcje magazynu: [Premium](../../storage/storage-premium-storage.md) (oparte na dysk SSD) i [standardowe](../../storage/storage-standard-storage.md) (oparte na dysk twardy).</span><span class="sxs-lookup"><span data-stu-id="ad160-104">Managed disks offers two storage options: [Premium](../../storage/storage-premium-storage.md) (SSD-based) and [Standard](../../storage/storage-standard-storage.md) (HDD-based).</span></span> <span data-ttu-id="ad160-105">Umożliwia ona łatwo przełączać się między dwie opcje z minimalnym czasem przestojów na podstawie Twoich potrzeb wydajności.</span><span class="sxs-lookup"><span data-stu-id="ad160-105">It allows you to easily switch between the two options with minimal downtime based on your performance needs.</span></span> <span data-ttu-id="ad160-106">Ta funkcja nie jest dostępna dla niezarządzanego dysków.</span><span class="sxs-lookup"><span data-stu-id="ad160-106">This capability is not available for unmanaged disks.</span></span> <span data-ttu-id="ad160-107">Ale możesz z łatwością [konwertować na zarządzane dyski](convert-unmanaged-to-managed-disks.md) można łatwo przełączać się między dwie opcje.</span><span class="sxs-lookup"><span data-stu-id="ad160-107">But you can easily [convert to managed disks](convert-unmanaged-to-managed-disks.md) to easily switch between the two options.</span></span>

<span data-ttu-id="ad160-108">W tym artykule przedstawiono sposób konwertowania dysków zarządzanych ze standardu do premium i na odwrót przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ad160-108">This article shows you how to convert managed disks from standard to premium, and vice versa by using Azure PowerShell.</span></span> <span data-ttu-id="ad160-109">Jeśli musisz zainstalować lub uaktualnić go, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="ad160-109">If you need to install or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ad160-110">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="ad160-110">Before you begin</span></span>

* <span data-ttu-id="ad160-111">Konwersja wymaga ponownego uruchomienia maszyny wirtualnej, więc planowanie migracji magazynu dysków w istniejącym oknie obsługi.</span><span class="sxs-lookup"><span data-stu-id="ad160-111">The conversion requires a restart of the VM, so schedule the migration of your disks storage during a pre-existing maintenance window.</span></span> 
* <span data-ttu-id="ad160-112">Jeśli używane są niezarządzane dysków, najpierw [konwertować na zarządzane dyski](convert-unmanaged-to-managed-disks.md) do korzystania z tego artykułu w celu przełączania się między dwie opcje magazynu.</span><span class="sxs-lookup"><span data-stu-id="ad160-112">If you are using unmanaged disks, first [convert to managed disks](convert-unmanaged-to-managed-disks.md) to use this article to switch between the two storage options.</span></span> 


## <a name="convert-all-the-managed-disks-of-a-vm-from-standard-to-premium-and-vice-versa"></a><span data-ttu-id="ad160-113">Konwertuj wszystkie zarządzane dyski maszyny wirtualnej ze standardu na — wersja premium i na odwrót</span><span class="sxs-lookup"><span data-stu-id="ad160-113">Convert all the managed disks of a VM from standard to premium, and vice versa</span></span>

<span data-ttu-id="ad160-114">W poniższym przykładzie zostanie przedstawiony sposób Przełącz wszystkie dyski maszyny Wirtualnej ze standardu, aby Magazyn w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="ad160-114">In the following example, we show how to switch all the disks of a VM from standard to premium storage.</span></span> <span data-ttu-id="ad160-115">Aby użyć dysków zarządzanych w warstwie premium, musisz użyć maszyny Wirtualnej [rozmiar maszyny Wirtualnej](sizes.md) obsługującym magazyn w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="ad160-115">To use premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="ad160-116">W tym przykładzie również zmienia rozmiar, który obsługuje magazyn w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="ad160-116">This example also switches to a size that supports premium storage.</span></span>

```powershell
# Name of the resource group that contains the VM
$rgName = 'yourResourceGroup'

# Name of the your virtual machine
$vmName = 'yourVM'

# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'

# Premium capable size
# Required only if converting storage from standard to premium
$size = 'Standard_DS2_v2'
$vm = Get-AzureRmVM -Name $vmName -resourceGroupName $rgName

# Stop and deallocate the VM before changing the size
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force

# Change the VM size to a size that supports premium storage
# Skip this step if converting storage from premium to standard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Get all disks in the resource group of the VM
$vmDisks = Get-AzureRmDisk -ResourceGroupName $rgName 

# For disks that belong to the selected VM, convert to premium storage
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
## <a name="convert-a-managed-disk-from-standard-to-premium-and-vice-versa"></a><span data-ttu-id="ad160-117">Konwertuj dysk zarządzanych ze standardu na — wersja premium i na odwrót</span><span class="sxs-lookup"><span data-stu-id="ad160-117">Convert a managed disk from standard to premium, and vice versa</span></span>

<span data-ttu-id="ad160-118">Dla obciążenia i testowania możesz mieć kombinację dysków warstwy standardowa i premium, aby zmniejszyć koszty.</span><span class="sxs-lookup"><span data-stu-id="ad160-118">For your dev/test workload, you may want to have mixture of standard and premium disks to reduce your cost.</span></span> <span data-ttu-id="ad160-119">Można wykonać je przez uaktualnienie do magazyn w warstwie premium, tylko dyski, które wymagają lepszą wydajność.</span><span class="sxs-lookup"><span data-stu-id="ad160-119">You can accomplish it by upgrading to premium storage, only the disks that require better performance.</span></span> <span data-ttu-id="ad160-120">W poniższym przykładzie zostanie przedstawiony sposób przełącznika jednego dysku maszyny Wirtualnej ze standardu, aby Magazyn w warstwie premium i na odwrót.</span><span class="sxs-lookup"><span data-stu-id="ad160-120">In the following example, we show how to switch a single disk of a VM from standard to premium storage, and vice versa.</span></span> <span data-ttu-id="ad160-121">Aby użyć dysków zarządzanych w warstwie premium, musisz użyć maszyny Wirtualnej [rozmiar maszyny Wirtualnej](sizes.md) obsługującym magazyn w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="ad160-121">To use premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="ad160-122">W tym przykładzie również zmienia rozmiar, który obsługuje magazyn w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="ad160-122">This example also switches to a size that supports premium storage.</span></span>

```powershell

$diskName = 'yourDiskName'
# resource group that contains the managed disk
$rgName = 'yourResourceGroupName'
# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'
# Premium capable size 
$size = 'Standard_DS2_v2'

$disk = Get-AzureRmDisk -DiskName $diskName -ResourceGroupName $rgName

# Get the ARM resource to get name and resource group of the VM
$vmResource = Get-AzureRmResource -ResourceId $disk.OwnerId
$vm = Get-AzureRmVM $vmResource.ResourceGroupName -Name $vmResource.ResourceName 

# Stop and deallocate the VM before changing the storage type
Stop-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name -Force

# Change the VM size to a size that supports premium storage
# Skip this step if converting storage from premium to standard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Update the storage type
$diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
-DiskName $disk.Name

Start-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name
```

## <a name="next-steps"></a><span data-ttu-id="ad160-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ad160-123">Next steps</span></span>

<span data-ttu-id="ad160-124">Podjąć tylko do odczytu kopię maszyny Wirtualnej za pomocą [migawki](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="ad160-124">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

