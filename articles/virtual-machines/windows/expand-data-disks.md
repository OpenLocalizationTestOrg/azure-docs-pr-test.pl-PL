---
title: "Zwiększ rozmiar dysku danych, dołączony do maszyny Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: "Zwiększyć rozmiar dysku danych, który jest dołączony do maszyny wirtualnej systemu Windows przy użyciu programu PowerShell."
services: virtual-machines-windows
documentationcenter: na
author: cynthn
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.openlocfilehash: 5529856c2ffcd2942fe3fc2b438f7e3fd16a67b2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="increase-the-size-of-a-data-disk-attached-to-a-windows-vm"></a>Zwiększ rozmiar dysku danych maszyny Wirtualnej systemu Windows

Jeśli musisz zwiększyć rozmiar dysku danych dołączona do maszyny wirtualnej, można zwiększyć rozmiar przy użyciu programu PowerShell. Po zwiększyć rozmiar dysku danych w ustawieniach maszyny Wirtualnej platformy Azure, należy przydzielić nowe miejsce na dysku w ramach maszyny Wirtualnej.


## <a name="use-powershell-to-increase-the-size-of-a-managed-data-disk"></a>Zwiększ rozmiar dysku danych zarządzanych przy użyciu programu Powershell

Aby zwiększyć rozmiar dysku danych zarządzanych, użyj następujących poleceń cmdlet programu PowerShell:

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [Get-AzureRMReseourceGroup](/powershell/module/azurerm.resources/get-azurermresourcegroup) | [Get-AzureRMVM](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [Stop-AzureRMVM](/powershell/module/azurerm.compute/stop-azurermvm)                        | [AzureRmDisk aktualizacji](/powershell/module/azurerm.compute/Update-AzureRmDisk) |
 | [Start AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm)             |
<br>

Poniższy skrypt przeprowadzi użytkownika przez proces pobierania informacji o maszyny Wirtualnej, wybierając dysku danych i określenie nowego rozmiaru.

```powershell
# Select resource group

    $rg = Get-AzureRMResourceGroup | Out-GridView `
        -Title "Select the resource group" `
        -PassThru

    $rgName = $rg.ResourceGroupName

# Select the VM

    $vm = Get-AzureRMVM -ResourceGroupName $rgName `
        | Out-GridView `
            -Title "Select a VM" `
             -PassThru

# Select data disk

    $disk = $vm.StorageProfile.DataDisks | Out-GridView `
        -Title "Select a data disk" `
        -PassThru

# Specify a larger size for the data disk

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior to resizing data disk

    $vm | Stop-AzureRMVM -Force

# Set the new disk size

    $diskUpdateConfig = New-AzureRmDiskUpdateConfig -DiskSizeGB $size

# Update the configuration in Azure

    $managedDisk = Get-AzureRmResource -ResourceId $disk.ManagedDisk.Id
    Update-AzureRmDisk -DiskName $managedDisk.ResourceName -ResourceGroupName $managedDisk.ResourceGroupName -DiskUpdate $diskUpdateConfig

# Start the VM

    Start-AzureRmVM -ResourceGroupName $rgName -VMName $vm.name
```

## <a name="use-powershell-to-increase-the-size-of-an-unmanaged-data-disk"></a>Zwiększ rozmiar dysku danych niezarządzanych za pomocą programu PowerShell

Aby zwiększyć rozmiar dysków niezarządzanych danych na koncie magazynu, należy użyć następujących poleceń cmdlet programu PowerShell:

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [Get-AzureRMStorageAccount](/powershell/module/azurerm.storage/get-azurermstorageaccount) | [Get-AzureRMVM](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [Stop-AzureRMVM](/powershell/module/azurerm.compute/stop-azurermvm)                       | [Zestaw AzureRmVMDataDisk](/powershell/module/azurerm.compute/set-azurermvmdatadisk) |
| [AzureRmVM aktualizacji](/powershell/module/azurerm.compute/update-azurermvm)                   | [Start AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm)             |

<br>

Poniższy skrypt umożliwia przeprowadzenie pobieranie maszyny Wirtualnej i magazynu informacje o koncie, wybierając dysku danych i określenie nowego rozmiaru.

```powershell

# Select Azure Storage Account

    $storageAccount =
        Get-AzureRMStorageAccount | Out-GridView `
            -Title "Select Azure Storage Account" `
            -PassThru

    $rgName = $storageAccount.ResourceGroupName

# Select the VM

    $vm = Get-AzureRMVM `
    -ResourceGroupName $rgName | Out-GridView `
            -Title "Select a VM …" `
            -PassThru

# Select Data Disk to resize

    $disk =
        $vm.DataDiskNames | Out-GridView `
            -Title "Select a data disk to resize" `
            -PassThru


# Specify a larger data disk size

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior to resizing data disk

    $vm | Stop-AzureRMVM -Force

# Set the new disk size

    Set-AzureRmVMDataDisk -VM $vm -Name "$disk" `
        -DiskSizeInGB $size

# Update the configuration in Azure

    Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Start the VM
    Start-AzureRmVM -ResourceGroupName $rgName `
    -VMName $vm.name

```

## <a name="allocate-the-unallocated-disk-space"></a>Przydziel nieprzydzielonego miejsca na dysku

Po utworzeniu dysku większy, należy przydzielić nowe nieprzydzielone miejsce z poziomu maszyny Wirtualnej. Aby przydzielić miejsce, można połączyć maszyny Wirtualnej użyj przystawki Zarządzanie dyskami (diskmgmt.msc). Lub, jeśli usługi WinRM i certyfikatu na maszynie Wirtualnej jest włączona podczas jego tworzenia, można użyć zdalnego programu PowerShell, aby zainicjalizować dysk. Można także użyć niestandardowego rozszerzenia skryptu:

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```

Plik skryptu może zawierać przypominać ten kod w celu zwiększenia przydziału dysków do maksymalnego rozmiaru dysków:

```powershell
$driveLetter= "F"

$MaxSize = (Get-PartitionSupportedSize -DriveLetter $driveLetter).sizeMax

Resize-Partition -DriveLetter $driveLetter -Size $MaxSize
```

## <a name="next-steps"></a>Następne kroki
- [Dowiedz się więcej o dyskach i wirtualne dyski twarde](../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
