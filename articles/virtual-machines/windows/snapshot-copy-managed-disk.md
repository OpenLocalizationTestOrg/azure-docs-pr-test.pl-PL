---
title: "Utwórz kopię dysku zarządzanego Azure dla kopii zapasowej | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć kopię dysku zarządzanego Azure na potrzeby kopii lub rozwiązywania problemów z dysku."
documentationcenter: 
author: cwatson-cat
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 15eb778e-fc07-45ef-bdc8-9090193a6d20
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 2/9/2017
ms.author: cwatson
ms.openlocfilehash: a7527b12f4f0d2b45713a0c0109d81ff51293fd8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a>Utwórz kopię plik VHD przechowywany jako dysk zarządzane Azure przy użyciu migawek zarządzane
Migawki zarządzane dysku do utworzenia kopii zapasowej lub Utwórz dysk zarządzane z migawki i dołączenie go do testowej maszyny wirtualnej, aby rozwiązać problemy. Zarządzane migawki jest kopią pełnej w momencie zarządzane dysku maszyny Wirtualnej. Tworzy kopię tylko do odczytu z wirtualnego dysku twardego i, domyślnie zapisuje go jako dysk standardowy zarządzane. Aby uzyskać więcej informacji o dyskach zarządzanych, zobacz [dysków zarządzanych Azure — omówienie](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

Aby uzyskać informacje o cenach, zobacz [cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/managed-disks/). 

## <a name="before-you-begin"></a>Przed rozpoczęciem
Jeśli używasz programu PowerShell, upewnij się, że masz najnowszą wersję modułu programu AzureRM.Compute PowerShell. Uruchom następujące polecenie, aby go zainstalować.

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).

## <a name="copy-the-vhd-with-a-snapshot"></a>Skopiuj wirtualny dysk twardy z migawki
Umożliwia utworzenie migawki dysków zarządzanych w portalu Azure lub programu PowerShell.

### <a name="use-azure-portal-to-take-a-snapshot"></a>Utworzenie migawki za pomocą portalu Azure 

1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).
2. Uruchamianie w lewym górnym rogu, kliknij przycisk **nowy** i wyszukaj **migawki**.
3. W bloku migawki kliknij **Utwórz**.
4. Wprowadź **nazwa** dla migawki.
5. Wybierz istniejącą [grupę zasobów](../../azure-resource-manager/resource-group-overview.md#resource-groups) lub wprowadź nazwę nowej grupy zasobów. 
6. Wybierz centrum danych Azure lokalizacji.  
7. Dla **dysku źródłowego**, wybierz zarządzany dysk do migawki.
8. Wybierz **typ konta** do przechowywania migawki. Firma Microsoft zaleca **Standard_LRS** chyba że ma być przechowywane na dysku wysokiej wydajności.
9. Kliknij przycisk **Utwórz**.

### <a name="use-powershell-to-take-a-snapshot"></a>Utworzenie migawki za pomocą programu PowerShell
Poniższe kroki pokazują jak uzyskać dysku VHD do skopiowania, Tworzenie migawki konfiguracji i migawki dysku za pomocą polecenia cmdlet New-AzureRmSnapshot<!--Add link to cmdlet when available-->. 

1. Ustaw niektórych parametrów. 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  Zastąp wartości parametrów:
  -  "myResourceGroup" z grupy zasobów maszyny Wirtualnej.
  -  "southeastasia" z lokalizacji geograficznej miejscu migawki zarządzane przechowywane. <!---How do you look these up? -->
  -  "ContosoMD_datadisk1" o nazwie dysku wirtualnego dysku twardego, który chcesz skopiować.
  -  "ContosoMD_datadisk1_snapshot1" o nazwie chcesz użyć dla nowej migawki.

2. Pobierz dysku VHD do skopiowania.

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. Tworzenie migawki konfiguracji. 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. Migawki.

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
Jeśli planujesz użyć migawki, aby utworzyć dysk zarządzany i dołączyć maszynę Wirtualną, która musi być wydajnych, użyj parametru `-AccountType Premium_LRS` przy użyciu polecenia New-AzureRmSnapshot. Parametr tworzy migawkę tak, aby była przechowywana jako dysk zarządzane Premium. Dysków zarządzanych w warstwie Premium są droższe niż standardowe. Dlatego upewnij się, że naprawdę potrzebny Premium przed użyciem tego parametru.


