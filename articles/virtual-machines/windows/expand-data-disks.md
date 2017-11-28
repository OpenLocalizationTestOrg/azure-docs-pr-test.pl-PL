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
# <a name="increase-hello-size-of-a-data-disk-attached-tooa-windows-vm"></a><span data-ttu-id="9418d-103">Zwiększ rozmiar dysku danych hello dołączony tooa maszyny Wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="9418d-103">Increase hello size of a data disk attached tooa Windows VM</span></span>

<span data-ttu-id="9418d-104">Jeśli potrzebujesz tooincrease hello rozmiar maszyny wirtualnej tooyour dysku danych hello, można zwiększyć rozmiar hello przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9418d-104">If you need tooincrease hello size of hello data disk attached tooyour virtual machine, you can increase hello size using PowerShell.</span></span> <span data-ttu-id="9418d-105">Po zwiększony rozmiar dysku danych hello w ustawieniach maszyny Wirtualnej Azure hello hello, należy również tooallocate hello nowego miejsca na dysku w ramach hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9418d-105">After you increase hello size of hello data disk in hello Azure VM settings, you also need tooallocate hello new disk space within hello VM.</span></span>


## <a name="use-powershell-tooincrease-hello-size-of-a-managed-data-disk"></a><span data-ttu-id="9418d-106">Użyj programu Powershell tooincrease hello rozmiar dysku danych zarządzanych</span><span class="sxs-lookup"><span data-stu-id="9418d-106">Use Powershell tooincrease hello size of a managed data disk</span></span>

<span data-ttu-id="9418d-107">tooincrease hello rozmiar dysku danych zarządzanych hello Użyj następującego polecenia cmdlet programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9418d-107">tooincrease hello size of a managed data disk, use hello following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="9418d-108">Get-AzureRMReseourceGroup</span><span class="sxs-lookup"><span data-stu-id="9418d-108">Get-AzureRMReseourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | [<span data-ttu-id="9418d-109">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="9418d-109">Get-AzureRMVM</span></span>](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [<span data-ttu-id="9418d-110">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="9418d-110">Stop-AzureRMVM</span></span>](/powershell/module/azurerm.compute/stop-azurermvm)                        | [<span data-ttu-id="9418d-111">AzureRmDisk aktualizacji</span><span class="sxs-lookup"><span data-stu-id="9418d-111">Update-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Update-AzureRmDisk) |
 | [<span data-ttu-id="9418d-112">Start AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="9418d-112">Start-AzureRmVM</span></span>](/powershell/module/azurerm.compute/start-azurermvm)             |
<br>

<span data-ttu-id="9418d-113">Hello poniższy skrypt przeprowadzi użytkownika przez proces pobierania informacji o hello maszyny Wirtualnej, wybierając hello dysku danych i określenie hello nowy rozmiar.</span><span class="sxs-lookup"><span data-stu-id="9418d-113">hello following script will walk you through getting hello VM information, selecting hello data disk and specifying hello new size.</span></span>

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

## <a name="use-powershell-tooincrease-hello-size-of-an-unmanaged-data-disk"></a><span data-ttu-id="9418d-114">Użyj programu PowerShell tooincrease hello rozmiar dysku danych niezarządzane</span><span class="sxs-lookup"><span data-stu-id="9418d-114">Use PowerShell tooincrease hello size of an unmanaged data disk</span></span>

<span data-ttu-id="9418d-115">rozmiar hello tooincrease dysków niezarządzanych danych na koncie magazynu, hello Użyj następującego polecenia cmdlet programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9418d-115">tooincrease hello size of unmanaged data disks in a storage account, use hello following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="9418d-116">Get-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="9418d-116">Get-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccount) | [<span data-ttu-id="9418d-117">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="9418d-117">Get-AzureRMVM</span></span>](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [<span data-ttu-id="9418d-118">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="9418d-118">Stop-AzureRMVM</span></span>](/powershell/module/azurerm.compute/stop-azurermvm)                       | [<span data-ttu-id="9418d-119">Zestaw AzureRmVMDataDisk</span><span class="sxs-lookup"><span data-stu-id="9418d-119">Set-AzureRmVMDataDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmdatadisk) |
| [<span data-ttu-id="9418d-120">AzureRmVM aktualizacji</span><span class="sxs-lookup"><span data-stu-id="9418d-120">Update-AzureRmVM</span></span>](/powershell/module/azurerm.compute/update-azurermvm)                   | [<span data-ttu-id="9418d-121">Start AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="9418d-121">Start-AzureRmVM</span></span>](/powershell/module/azurerm.compute/start-azurermvm)             |

<br>

<span data-ttu-id="9418d-122">Witaj poniższy skrypt prowadzi użytkownika przez proces uzyskiwania hello maszyny Wirtualnej i magazynu informacji o koncie, wybierając hello dysku danych i określenie hello nowy rozmiar.</span><span class="sxs-lookup"><span data-stu-id="9418d-122">hello following script will walk you through getting hello VM and storage account information, selecting hello data disk and specifying hello new size.</span></span>

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

## <a name="allocate-hello-unallocated-disk-space"></a><span data-ttu-id="9418d-123">Przydziel hello nieprzydzielonego miejsca na dysku</span><span class="sxs-lookup"><span data-stu-id="9418d-123">Allocate hello unallocated disk space</span></span>

<span data-ttu-id="9418d-124">Po utworzeniu dysku hello większy, należy tooallocate hello nowe nieprzydzielone miejsce z wewnątrz hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9418d-124">Once you have made hello drive larger, you need tooallocate hello new unallocated space from within hello VM.</span></span> <span data-ttu-id="9418d-125">tooallocate hello miejsca, możesz połączyć toohello maszyny Wirtualnej użyj przystawki Zarządzanie dyskami (diskmgmt.msc).</span><span class="sxs-lookup"><span data-stu-id="9418d-125">tooallocate hello space, you can connect toohello VM use Disk Management (diskmgmt.msc).</span></span> <span data-ttu-id="9418d-126">Lub, jeśli usługi WinRM i certyfikatu na powitania maszyny Wirtualnej jest włączona podczas jego tworzenia, możesz użyć zdalnego programu PowerShell tooinitialize hello dysku.</span><span class="sxs-lookup"><span data-stu-id="9418d-126">Or, if you enabled WinRM and a certificate on hello VM when you created it, you can use remote PowerShell tooinitialize hello disk.</span></span> <span data-ttu-id="9418d-127">Można także użyć niestandardowego rozszerzenia skryptu:</span><span class="sxs-lookup"><span data-stu-id="9418d-127">You can also use a custom script extension:</span></span>

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```

<span data-ttu-id="9418d-128">plik skryptu Hello może zawierać przypominać ten kod tooincrease hello dysku alokacji toohello maksymalny rozmiar hello dysków:</span><span class="sxs-lookup"><span data-stu-id="9418d-128">hello script file can contain something like this code tooincrease hello drive allocation toohello maximum size hello disks:</span></span>

```powershell
$driveLetter= "F"

$MaxSize = (Get-PartitionSupportedSize -DriveLetter $driveLetter).sizeMax

Resize-Partition -DriveLetter $driveLetter -Size $MaxSize
```

## <a name="next-steps"></a><span data-ttu-id="9418d-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9418d-129">Next Steps</span></span>
- [<span data-ttu-id="9418d-130">Dowiedz się więcej o dyskach i wirtualne dyski twarde</span><span class="sxs-lookup"><span data-stu-id="9418d-130">Learn more about disks and VHDs</span></span>](../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
