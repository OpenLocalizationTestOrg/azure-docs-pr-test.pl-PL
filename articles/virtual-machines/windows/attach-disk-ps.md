---
title: "aaaAttach tooa dysku danych maszyny Wirtualnej systemu Windows na platformie Azure przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Jak tooattach danych nowego lub istniejącego dysku tooa maszyny Wirtualnej systemu Windows przy użyciu programu PowerShell z modelu wdrażania usługi Resource Manager hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: cynthn
ms.openlocfilehash: 12ffdd4ced791ba0948047d3af24ad73e36c7ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-vm-using-powershell"></a>Dołącz tooa dysku danych maszyny Wirtualnej systemu Windows przy użyciu programu PowerShell

W tym artykule opisano, jak tooattach istniejących i nowych dysków maszyny wirtualnej systemu Windows tooa przy użyciu programu PowerShell. Jeśli maszyna wirtualna używa dysków zarządzanych, możesz dołączyć dyski dodatkowych danych zarządzanych. Można również dołączyć niezarządzanych danych tooa dysków maszyny Wirtualnej używającej dysków niezarządzanego na koncie magazynu.

Zanim to zrobisz, przejrzyj następujące wskazówki:
* Hello rozmiar maszyny wirtualnej hello Określa, ile można dołączać dysków z danymi. Aby uzyskać więcej informacji, zobacz [rozmiary maszyn wirtualnych](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Magazyn w warstwie Premium toouse, będziesz potrzebować magazyn w warstwie Premium włączone rozmiar maszyny Wirtualnej, takie jak hello serii DS lub GS-series maszyny wirtualnej. Z tych maszyn wirtualnych służy dysków z konta magazynu zarówno Premium i standardowa. Magazyn w warstwie Premium jest dostępna w pewnych regionach. Aby uzyskać więcej informacji, zobacz [magazyn w warstwie Premium: magazyn o wysokiej wydajności dla obciążeń maszyny wirtualnej Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="before-you-begin"></a>Przed rozpoczęciem
Jeśli używasz programu PowerShell, upewnij się, że masz najnowszą wersję hello modułu AzureRM.Compute PowerShell hello. Uruchom hello następujących tooinstall polecenia.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).


## <a name="add-an-empty-data-disk-tooa-virtual-machine"></a>Dodaj maszynę wirtualną tooa danych pusty dysk

Ten przykład przedstawia, jak tooadd pustymi danymi dysku tooan istniejącej maszyny wirtualnej.

### <a name="using-managed-disks"></a>Za pomocą dysków zarządzanych

```powershell
$rgName = 'myResourceGroup'
$vmName = 'myVM'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk1'

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Empty -DiskSizeGB 128

$dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

### <a name="using-unmanaged-disks-in-a-storage-account"></a>Za pomocą niezarządzanych dysków na koncie magazynu

```powershell
    $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    Add-AzureRmVMDataDisk -VM $vm -Name "disk-name" -VhdUri "https://mystore1.blob.core.windows.net/vhds/datadisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
    Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
```


### <a name="initialize-hello-disk"></a>Inicjowanie dysku hello

Po dodaniu pusty dysk należy tooinitialize go. tooinitialize hello dysku, można rejestrować w usłudze zarządzania dyskami maszyny Wirtualnej i użyj tooa. Jeśli usługi WinRM i certyfikatu na powitania maszyny Wirtualnej jest włączona podczas jego tworzenia, możesz użyć zdalnego programu PowerShell tooinitialize hello dysku. Można także użyć niestandardowego rozszerzenia skryptu: 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
plik skryptu Hello może zawierać przypominać ten kod tooinitialize hello dysków:

```powershell
    $disks = Get-Disk | Where partitionstyle -eq 'raw' | sort number

    $letters = 70..89 | ForEach-Object { [char]$_ }
    $count = 0
    $labels = "data1","data2"

    foreach ($disk in $disks) {
        $driveLetter = $letters[$count].ToString()
        $disk | 
        Initialize-Disk -PartitionStyle MBR -PassThru |
        New-Partition -UseMaximumSize -DriveLetter $driveLetter |
        Format-Volume -FileSystem NTFS -NewFileSystemLabel $labels[$count] -Confirm:$false -Force
    $count++
    }
```


## <a name="attach-an-existing-data-disk-tooa-vm"></a>Dołączanie istniejącego tooa dysku danych maszyny Wirtualnej

Można również dołączyć istniejącego dysku VHD, jako maszynę wirtualną tooa dysku danych zarządzanych. 

### <a name="using-managed-disks"></a>Za pomocą dysków zarządzanych

```powershell
$rgName = 'myRG'
$vmName = 'ContosoMdPir3'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk2'
$dataVhdUri = 'https://mystorageaccount.blob.core.windows.net/vhds/managed_data_disk.vhd' 

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Import -SourceUri $dataVhdUri -DiskSizeGB 128

$dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk2.Id -Lun 2

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

## <a name="next-steps"></a>Następne kroki

Utwórz [migawki](snapshot-copy-managed-disk.md).
