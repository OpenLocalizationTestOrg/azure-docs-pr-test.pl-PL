---
title: "Tworzenie dysku zarządzanego z dysku VHD na platformie Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie dysku zarządzanego z dysku VHD, które jest obecnie kontem magazynu platformy Azure przy użyciu modelu wdrażania Menedżera zasobów."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: cynthn
ms.openlocfilehash: c03ebf73f1090b595149daf2eb3e274b05822f4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a>Tworzenie dysków zarządzanych z niezarządzanego dysków na koncie magazynu

Dysk zarządzany mogą być tworzone z istniejącego dysku danych lub dysk systemu operacyjnego, które jest obecnie konta magazynu platformy Azure. Można również utworzyć pusty dysk, który może służyć jako nowego dysku danych maszyny Wirtualnej. 

## <a name="before-you-begin"></a>Przed rozpoczęciem
Jeśli używasz programu PowerShell, upewnij się, że masz najnowszą wersję modułu programu AzureRM.Compute PowerShell. Uruchom następujące polecenie, aby go zainstalować.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a>Tworzenie dysku zarządzanego z dysku VHD w koncie magazynu platformy Azure

W tym przykładzie, możemy utworzyć dysk z wirtualnego dysku twardego zarządzanego dysku i przypisz je do parametru **$ dysk 1** do użycia w przyszłości. 

Zostaną utworzone dysków zarządzanych w **zachodnie-US** lokalizacji, w grupie zasobów o nazwie **myResourceGroup**. Dysk będzie miała nazwę **myDisk** i zostanie utworzony z pliku wirtualnego dysku twardego o nazwie **myDisk.vhd** możemy wcześniej przekazany do konta magazynu o nazwie **mojekontomagazynu**. Zostanie utworzona dysków zarządzanych w warstwie premium magazyn lokalnie nadmiarowy (LRS). StandardLRS i PremiumLRS są tylko **- AccountType** opcje dostępne dla zarządzanych dysków. 

1.  Ustaw niektórych parametrów

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. Utwórz dysk z danymi. 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a>Utwórz dysk danych puste jako dysków zarządzanych

W tym przykładzie firma Microsoft Utwórz dysk danych puste jako dysków zarządzanych i przypisz je do parametru **$dataDisk2** do użycia w przyszłości. Musi być zainicjowana logowanie do maszyny Wirtualnej i przy użyciu diskmgmt.msc dysku danych puste lub [zdalnie za pomocą usługi WinRM i skrypt](attach-disk-ps.md#initialize-the-disk), gdy jest on dołączony do uruchomionej maszyny Wirtualnej.

Dysk z danymi puste, zostanie utworzony w **zachodnie centralnej nam** lokalizacji, w grupie zasobów o nazwie **myResourceGroup**. Dysk będzie miała nazwę **myEmptyDataDisk**. Pusty dysk zostanie utworzony w warstwie premium magazyn lokalnie nadmiarowy (LRS). StandardLRS i PremiumLRS są tylko **- AccountType** opcje dostępne dla zarządzanych dysków.

Rozmiar dysku w tym przykładzie jest 128GB, ale należy wybrać rozmiar, które zaspokoi potrzeby wszystkie aplikacje uruchomione na maszynie Wirtualnej.

1.  Ustaw niektórych parametrów

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. Utwórz dysk z danymi.
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a>Następne kroki   
- Jeśli masz już Maszynę wirtualną, możesz [dołączenie dysku danych](attach-disk-portal.md).
