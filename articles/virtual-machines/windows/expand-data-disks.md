---
title: "aaaExpand dysku danych dołączona tooa maszyny Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: "Rozwiń hello rozmiar dysku danych maszyny wirtualnej systemu Windows tooa dołączone przy użyciu programu PowerShell."
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
ms.openlocfilehash: b16ad0da9cff9dfffc9dc9ec7dd72891e7ddd745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="increase-hello-size-of-a-data-disk-attached-tooa-windows-vm"></a>Zwiększ rozmiar dysku danych hello dołączony tooa maszyny Wirtualnej systemu Windows

Jeśli potrzebujesz tooincrease hello rozmiar maszyny wirtualnej tooyour dysku danych hello, można zwiększyć rozmiar hello przy użyciu programu PowerShell. Po zwiększony rozmiar dysku danych hello w ustawieniach maszyny Wirtualnej Azure hello hello, należy również tooallocate hello nowego miejsca na dysku w ramach hello maszyny Wirtualnej.


## <a name="use-powershell-tooincrease-hello-size-of-a-managed-data-disk"></a>Użyj programu Powershell tooincrease hello rozmiar dysku danych zarządzanych

tooincrease hello rozmiar dysku danych zarządzanych hello Użyj następującego polecenia cmdlet programu PowerShell:

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [Get-AzureRMReseourceGroup](/powershell/module/azurerm.resources/get-azurermresourcegroup) | [Get-AzureRMVM](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [Stop-AzureRMVM](/powershell/module/azurerm.compute/stop-azurermvm)                        | [AzureRmDisk aktualizacji](/powershell/module/azurerm.compute/Update-AzureRmDisk) |
 | [Start AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm)             |
<br>

Hello poniższy skrypt przeprowadzi użytkownika przez proces pobierania informacji o hello maszyny Wirtualnej, wybierając hello dysku danych i określenie hello nowy rozmiar.

```powershell
# Select resource group

    $rg = Get-AzureRMResourceGroup | Out-GridView `
        -Title "Select hello resource group" `
        -PassThru

    $rgName = $rg.ResourceGroupName

# Select hello VM

    $vm = Get-AzureRMVM -ResourceGroupName $rgName `
        | Out-GridView `
            -Title "Select a VM" `
             -PassThru

# Select data disk

    $disk = $vm.StorageProfile.DataDisks | Out-GridView `
        -Title "Select a data disk" `
        -PassThru

# Specify a larger size for hello data disk

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior tooresizing data disk

    $vm | Stop-AzureRMVM -Force

# Set hello new disk size

    $diskUpdateConfig = New-AzureRmDiskUpdateConfig -DiskSizeGB $size

# Update hello configuration in Azure

    $managedDisk = Get-AzureRmResource -ResourceId $disk.ManagedDisk.Id
    Update-AzureRmDisk -DiskName $managedDisk.ResourceName -ResourceGroupName $managedDisk.ResourceGroupName -DiskUpdate $diskUpdateConfig

# Start hello VM

    Start-AzureRmVM -ResourceGroupName $rgName -VMName $vm.name
```

## <a name="use-powershell-tooincrease-hello-size-of-an-unmanaged-data-disk"></a>Użyj programu PowerShell tooincrease hello rozmiar dysku danych niezarządzane

rozmiar hello tooincrease dysków niezarządzanych danych na koncie magazynu, hello Użyj następującego polecenia cmdlet programu PowerShell:

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [Get-AzureRMStorageAccount](/powershell/module/azurerm.storage/get-azurermstorageaccount) | [Get-AzureRMVM](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [Stop-AzureRMVM](/powershell/module/azurerm.compute/stop-azurermvm)                       | [Zestaw AzureRmVMDataDisk](/powershell/module/azurerm.compute/set-azurermvmdatadisk) |
| [AzureRmVM aktualizacji](/powershell/module/azurerm.compute/update-azurermvm)                   | [Start AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm)             |

<br>

Witaj poniższy skrypt prowadzi użytkownika przez proces uzyskiwania hello maszyny Wirtualnej i magazynu informacji o koncie, wybierając hello dysku danych i określenie hello nowy rozmiar.

```powershell

# Select Azure Storage Account

    $storageAccount =
        Get-AzureRMStorageAccount | Out-GridView `
            -Title "Select Azure Storage Account" `
            -PassThru

    $rgName = $storageAccount.ResourceGroupName

# Select hello VM

    $vm = Get-AzureRMVM `
    -ResourceGroupName $rgName | Out-GridView `
            -Title "Select a VM …" `
            -PassThru

# Select Data Disk tooresize

    $disk =
        $vm.DataDiskNames | Out-GridView `
            -Title "Select a data disk tooresize" `
            -PassThru


# Specify a larger data disk size

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior tooresizing data disk

    $vm | Stop-AzureRMVM -Force

# Set hello new disk size

    Set-AzureRmVMDataDisk -VM $vm -Name "$disk" `
        -DiskSizeInGB $size

# Update hello configuration in Azure

    Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Start hello VM
    Start-AzureRmVM -ResourceGroupName $rgName `
    -VMName $vm.name

```

## <a name="allocate-hello-unallocated-disk-space"></a>Przydziel hello nieprzydzielonego miejsca na dysku

Po utworzeniu dysku hello większy, należy tooallocate hello nowe nieprzydzielone miejsce z wewnątrz hello maszyny Wirtualnej. tooallocate hello miejsca, możesz połączyć toohello maszyny Wirtualnej użyj przystawki Zarządzanie dyskami (diskmgmt.msc). Lub, jeśli usługi WinRM i certyfikatu na powitania maszyny Wirtualnej jest włączona podczas jego tworzenia, możesz użyć zdalnego programu PowerShell tooinitialize hello dysku. Można także użyć niestandardowego rozszerzenia skryptu:

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```

plik skryptu Hello może zawierać przypominać ten kod tooincrease hello dysku alokacji toohello maksymalny rozmiar hello dysków:

```powershell
$driveLetter= "F"

$MaxSize = (Get-PartitionSupportedSize -DriveLetter $driveLetter).sizeMax

Resize-Partition -DriveLetter $driveLetter -Size $MaxSize
```

## <a name="next-steps"></a>Następne kroki
- [Dowiedz się więcej o dyskach i wirtualne dyski twarde](../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
