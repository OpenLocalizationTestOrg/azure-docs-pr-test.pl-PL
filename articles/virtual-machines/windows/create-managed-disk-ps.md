---
title: "aaaCreate dysków zarządzanych z dysku VHD na platformie Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie dysku zarządzanego z dysku VHD, które jest obecnie kontem magazynu platformy Azure przy użyciu modelu wdrażania usługi Resource Manager hello."
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
ms.openlocfilehash: 77adaac5419186ff85039fe2c4752f021aa5e448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a>Tworzenie dysków zarządzanych z niezarządzanego dysków na koncie magazynu

Dysk zarządzany mogą być tworzone z istniejącego dysku danych lub dysk systemu operacyjnego, które jest obecnie konta magazynu platformy Azure. Można również utworzyć pusty dysk, który może służyć jako nowego dysku danych maszyny Wirtualnej. 

## <a name="before-you-begin"></a>Przed rozpoczęciem
Jeśli używasz programu PowerShell, upewnij się, że masz najnowszą wersję hello modułu AzureRM.Compute PowerShell hello. Uruchom hello następujących tooinstall polecenia.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a>Tworzenie dysku zarządzanego z dysku VHD w koncie magazynu platformy Azure

W przykładzie hello możemy utworzyć dysk z wirtualnego dysku twardego dysków zarządzanych i przypisz do niego parametru toohello **dysk 1 $** toouse później. 

Witaj dysków zarządzanych zostaną utworzone w hello **zachodnie-US** lokalizacji, w grupie zasobów o nazwie **myResourceGroup**. Witaj dysku będzie miała nazwę **myDisk** i zostanie utworzony z pliku wirtualnego dysku twardego o nazwie **myDisk.vhd** możemy wcześniej przekazany tooa konto magazynu o nazwie **mojekontomagazynu**. zostanie utworzona Hello dysków zarządzanych w warstwie premium magazyn lokalnie nadmiarowy (LRS). StandardLRS i PremiumLRS są tylko hello **- AccountType** opcje dostępne dla zarządzanych dysków. 

1.  Ustaw niektórych parametrów

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. Utwórz dysk danych hello. 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a>Utwórz dysk danych puste jako dysków zarządzanych

W przykładzie hello możemy utworzyć dysk danych puste jako dysków zarządzanych w i przypisz do niego parametru toohello **$dataDisk2** toouse później. Dysku danych puste, należy zainicjować toobe logowanie toohello maszyny Wirtualnej i przy użyciu diskmgmt.msc lub [zdalnie za pomocą usługi WinRM i skrypt](attach-disk-ps.md#initialize-the-disk), po dołączonych tooa uruchamiania maszyny Wirtualnej.

Hello danych pusty dysk zostanie utworzony w hello **zachodnie centralnej nam** lokalizacji, w grupie zasobów o nazwie **myResourceGroup**. Witaj dysku będzie miała nazwę **myEmptyDataDisk**. pusty dysk Hello zostaną utworzone w warstwie premium magazyn lokalnie nadmiarowy (LRS). StandardLRS i PremiumLRS są tylko hello **- AccountType** opcje dostępne dla zarządzanych dysków.

rozmiar dysku Hello w tym przykładzie jest 128GB, ale należy wybrać rozmiar, który spełnia potrzeby hello wszystkie aplikacje uruchomione na maszynie Wirtualnej.

1.  Ustaw niektórych parametrów

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. Utwórz dysk danych hello.
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a>Następne kroki   
- Jeśli masz już Maszynę wirtualną, możesz [dołączenie dysku danych](attach-disk-portal.md).
