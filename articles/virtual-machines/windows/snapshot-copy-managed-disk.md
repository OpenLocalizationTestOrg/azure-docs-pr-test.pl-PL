---
title: "aaaCreate kopii dysku zarządzanego Azure wykonywać kopie zapasowe | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate kopię toouse Azure zarządzanych dysku dla dysku z powrotem się lub rozwiązywania problemów problemy."
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
ms.openlocfilehash: 2f33dbbee624bcd813f3c7c3e3401072d0933714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a>Utwórz kopię plik VHD przechowywany jako dysk zarządzane Azure przy użyciu migawek zarządzane
Migawki zarządzane dysku do utworzenia kopii zapasowej lub Utwórz dysk zarządzane z migawki hello i dołączenie go tooa test maszyny wirtualnej tootroubleshoot. Zarządzane migawki jest kopią pełnej w momencie zarządzane dysku maszyny Wirtualnej. Tworzy kopię tylko do odczytu z wirtualnego dysku twardego i, domyślnie zapisuje go jako dysk standardowy zarządzane. Aby uzyskać więcej informacji o dyskach zarządzanych, zobacz [dysków zarządzanych Azure — omówienie](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

Aby uzyskać informacje o cenach, zobacz [cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/managed-disks/). 

## <a name="before-you-begin"></a>Przed rozpoczęciem
Jeśli używasz programu PowerShell, upewnij się, że masz najnowszą wersję hello modułu AzureRM.Compute PowerShell hello. Uruchom hello następujących tooinstall polecenia.

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).

## <a name="copy-hello-vhd-with-a-snapshot"></a>Skopiuj hello wirtualnego dysku twardego z migawki
Użyj hello portalu Azure lub programu PowerShell tootake migawkę hello dysku zarządzanego.

### <a name="use-azure-portal-tootake-a-snapshot"></a>Użyj tootake portalu Azure migawki 

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Począwszy od lewego górnego rogu powitania kliknij **nowy** i wyszukaj **migawki**.
3. W bloku migawki powitania kliknij **Utwórz**.
4. Wprowadź **nazwa** hello migawki.
5. Wybierz istniejący [grupy zasobów](../../azure-resource-manager/resource-group-overview.md#resource-groups) lub nazwa typu hello nowej. 
6. Wybierz centrum danych Azure lokalizacji.  
7. Aby uzyskać **dysku źródłowego**, wybierz hello toosnapshot dysku zarządzanego.
8. Wybierz hello **typ konta** toouse toostore hello migawki. Firma Microsoft zaleca **Standard_LRS** chyba że ma być przechowywane na dysku wysokiej wydajności.
9. Kliknij przycisk **Utwórz**.

### <a name="use-powershell-tootake-a-snapshot"></a>Użyj programu PowerShell tootake migawki
Witaj następujące kroki pokazują, jak hello tooget wirtualnego dysku twardego na dysku toobe kopiowane, tworzyć hello konfiguracje migawek i migawki hello dysku za pomocą polecenia cmdlet hello AzureRmSnapshot nowy<!--Add link toocmdlet when available-->. 

1. Ustaw niektórych parametrów. 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  Zastąp wartości parametrów hello:
  -  "myResourceGroup" hello wirtualna grupą zasobów.
  -  "southeastasia" z lokalizacji geograficznej hello miejscu migawki zarządzane przechowywane. <!---How do you look these up? -->
  -  "ContosoMD_datadisk1" o nazwie hello hello dysku VHD, które mają toocopy.
  -  Nazwa "ContosoMD_datadisk1_snapshot1" z hello mają toouse dla hello nową migawkę.

2. Pobierz toobe dysku VHD hello skopiowane.

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. Utwórz hello konfiguracje migawek. 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. Witaj migawki.

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
Jeśli planujesz toouse hello migawki toocreate dysku zarządzanego dołączyć maszynę Wirtualną, która wymaga wydajnych toobe, użyj parametru hello `-AccountType Premium_LRS` za pomocą polecenia hello AzureRmSnapshot nowy. Parametr Hello tworzy migawkę hello, aby są przechowywane jako dysk zarządzane Premium. Dysków zarządzanych w warstwie Premium są droższe niż standardowe. Dlatego upewnij się, że naprawdę potrzebny Premium przed użyciem tego parametru.


