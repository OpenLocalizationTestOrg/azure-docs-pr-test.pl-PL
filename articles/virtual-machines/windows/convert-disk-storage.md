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
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a>Konwertuj Azure zarządzanego magazynu dysków z toopremium standardowe i na odwrót

Zarządzane dysków oferuje dwie opcje magazynu: [Premium](../../storage/storage-premium-storage.md) (oparte na dysk SSD) i [standardowe](../../storage/storage-standard-storage.md) (oparte na dysk twardy). Pozwala ona tooeasily przełączanie między Witaj dwie opcje z minimalnym czasem przestojów na podstawie Twoich potrzeb wydajności. Ta funkcja nie jest dostępna dla niezarządzanego dysków. Ale możesz z łatwością [skonwertuj dyski toomanaged](convert-unmanaged-to-managed-disks.md) tooeasily przełączanie między Witaj dwie opcje.

W tym artykule opisano sposób tooconvert zarządzania dysków z toopremium standardowe i na odwrót przy użyciu programu Azure PowerShell. Jeśli konieczne tooinstall lub uaktualnić go, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/install-azurerm-ps.md).

## <a name="before-you-begin"></a>Przed rozpoczęciem

* Hello konwersja wymaga ponownego uruchomienia hello maszyny Wirtualnej, więc planowanie migracji hello magazynu dysków w istniejącym oknie obsługi. 
* Jeśli używane są niezarządzane dysków, najpierw [skonwertuj dyski toomanaged](convert-unmanaged-to-managed-disks.md) toouse tooswitch tego artykułu między Witaj dwie opcje magazynu. 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a>Konwertuj hello wszystkie zarządzane dyski maszyny wirtualnej z toopremium standardowe i na odwrót

W hello poniższy przykład, zostanie przedstawiony sposób tooswitch hello wszystkie dyski maszyny Wirtualnej z magazynu standardowego toopremium. toouse premium zarządzane dyski, należy użyć maszyny Wirtualnej [rozmiar maszyny Wirtualnej](sizes.md) obsługującym magazyn w warstwie premium. W tym przykładzie również zmienia rozmiar tooa, który obsługuje magazyn w warstwie premium.

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
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a>Konwertuj dysk zarządzanego z toopremium standardowe i na odwrót

Dla obciążenia i testowania możesz toohave kombinację dysków warstwy standardowa i premium tooreduce koszt. Można wykonać je przez uaktualnienie magazynu toopremium tylko dyski hello, które wymagają lepszą wydajność. W hello poniższy przykład, zostanie przedstawiony sposób tooswitch jednego dysku maszyny wirtualnej z magazynu standardowego toopremium i na odwrót. toouse premium zarządzane dyski, należy użyć maszyny Wirtualnej [rozmiar maszyny Wirtualnej](sizes.md) obsługującym magazyn w warstwie premium. W tym przykładzie również zmienia rozmiar tooa, który obsługuje magazyn w warstwie premium.

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

## <a name="next-steps"></a>Następne kroki

Podjąć tylko do odczytu kopię maszyny Wirtualnej za pomocą [migawki](snapshot-copy-managed-disk.md).

