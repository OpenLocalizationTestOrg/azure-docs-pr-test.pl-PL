---
title: dyski aaaManage Azure z hello Azure PowerShell | Dokumentacja firmy Microsoft
description: "Samouczek — Zarządzanie dyskami Azure z hello Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 2f61ad18bc94bab527d7ae593da603c6073adc89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-powershell"></a>Zarządzanie dyskami Azure przy użyciu programu PowerShell

Maszyny wirtualne platformy Azure, użyj systemu operacyjnego dyski toostore hello maszyn wirtualnych, aplikacji i danych. Podczas tworzenia maszyny Wirtualnej jest ważne toochoose rozmiar dysku i obciążenia odpowiednie toohello oczekiwano konfiguracji. W tym samouczku opisano wdrażanie i Zarządzanie dyskami maszyny Wirtualnej. Informacje o:

> [!div class="checklist"]
> * Dyski systemu operacyjnego i tymczasowego
> * Dyski danych
> * Standard i dysków w warstwie Premium
> * Wydajność dysku
> * Dołączanie i przygotowywania dysków z danymi

Ten samouczek wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej. Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji. Jeśli potrzebujesz tooupgrade, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="default-azure-disks"></a>Domyślna dysku systemu Azure

Po utworzeniu maszyny wirtualnej platformy Azure, dwa dyski są automatycznie dołączone toohello maszyny wirtualnej. 

**Dysk systemu operacyjnego** — dysków systemu operacyjnego mogą być określane w górę terabajt too1 i hosty hello maszyn wirtualnych systemu operacyjnego.  dysk systemu operacyjnego Hello jest przypisanej litery dysku z *c:* domyślnie. Witaj dyskowej pamięci podręcznej konfiguracji dysku systemu operacyjnego hello jest zoptymalizowana pod kątem wydajności systemu operacyjnego. dysk systemu operacyjnego Hello **nie powinien** hosta aplikacji i danych. Dla aplikacji i danych należy użyć dysku danych, które szczegółowo w dalszej części tego artykułu.

**Dysku tymczasowym** -tymczasowego dysków używać dysków SSD, który znajduje się na powitania tego samego hosta platformy Azure jako hello maszyny Wirtualnej. Tymczasowy dyski są wysokiej wydajności i mogą być używane do operacji, takich jak przetwarzanie danych tymczasowych. Jednak hello maszyny Wirtualnej w przypadku tooa przeniesiony na nowy host, zostaną usunięte wszystkie dane przechowywane na dysku tymczasowym. rozmiar dysku tymczasowym hello Hello jest określana przez hello rozmiar maszyny Wirtualnej. Tymczasowe dyski są przypisane literę dysku *d:* domyślnie.

### <a name="temporary-disk-sizes"></a>Rozmiary dysku tymczasowym

| Typ | Rozmiar maszyny Wirtualnej | Maksymalny rozmiar dysku tymczasowego (GB) |
|----|----|----|
| [Zastosowania ogólne](sizes-general.md) | A i serii D | 800 |
| [Optymalizacja pod kątem obliczeń](sizes-compute.md) | Seria F | 800 |
| [Optymalizacja pod kątem pamięci](../virtual-machines-windows-sizes-memory.md) | D i G serii | 6144 |
| [Optymalizacja pod kątem magazynu](../virtual-machines-windows-sizes-storage.md) | Seria L | 5630 |
| [Procesor GPU](sizes-gpu.md) | N serii | 1440 |
| [Wysoka wydajność](sizes-hpc.md) | A i serii H | 2000 |

## <a name="azure-data-disks"></a>Dyski danych Azure

Instalowanie aplikacji i przechowywania danych można dodać dodatkowego dysku z danymi. Dyski danych używanego w sytuacji, gdy wymagane jest trwałe i szybko reagowały pamięci masowej. Każdy dysk danych ma maksymalną pojemność 1 terabajt. rozmiar Hello hello maszyny wirtualnej Określa, jak wiele dysków z danymi mogą być dołączone tooa maszyny Wirtualnej. Dla każdej podstawowej maszyny Wirtualnej można dołączyć danych dwóch dysków. 

### <a name="max-data-disks-per-vm"></a>Maksymalna liczba dysków z danymi dla maszyny Wirtualnej

| Typ | Rozmiar maszyny Wirtualnej | Maksymalna liczba dysków z danymi dla maszyny Wirtualnej |
|----|----|----|
| [Zastosowania ogólne](sizes-general.md) | A i serii D | 32 |
| [Optymalizacja pod kątem obliczeń](sizes-compute.md) | Seria F | 32 |
| [Optymalizacja pod kątem pamięci](../virtual-machines-windows-sizes-memory.md) | D i G serii | 64 |
| [Optymalizacja pod kątem magazynu](../virtual-machines-windows-sizes-storage.md) | Seria L | 64 |
| [Procesor GPU](sizes-gpu.md) | N serii | 48 |
| [Wysoka wydajność](sizes-hpc.md) | A i serii H | 32 |

## <a name="vm-disk-types"></a>Typy dysków maszyny Wirtualnej

Platforma Azure oferuje dwa rodzaje dysku.

### <a name="standard-disk"></a>Dysków w warstwie standardowa

Magazyn Standard Storage bazuje na dyskach twardych (HDD) i stanowi ekonomiczne, chociaż wciąż wydajne rozwiązanie. Dyski standardowe idealnie nadają się do deweloperów ekonomiczne i testów obciążenia.

### <a name="premium-disk"></a>Dysku Premium

Dyski Premium bazują na dysk SSD dysku wysokiej wydajności i małych opóźnień. Idealny dla maszyn wirtualnych obciążeniu produkcji. Magazyn w warstwie Premium obsługuje serii DS, DSv2 serii GS-series i FS serii maszyn wirtualnych. Dysków w warstwie Premium są dostępne w trzech typów (P10, P20, P30), rozmiar hello dysku hello Określa typ dysku hello. Podczas wybierania, wartość hello rozmiaru dysku jest zaokrąglana toohello dalej typu. Na przykład jeśli rozmiar hello jest poniżej typ dysku hello 128 GB będzie P10, między 129 i 512 P20 i ponad 512 P30. 

### <a name="premium-disk-performance"></a>Wydajność dysku Premium

|Typ dysku magazynu w warstwie Premium | P10 | P20 | P30 |
| --- | --- | --- | --- |
| Rozmiar dysku (zaokrąglony) | 128 GB | 512 GB | 1024 GB (1 TB) |
| Liczba operacji wejścia/wyjścia na sekundę na dysk | 500 | 2,300 | 5,000 |
Przepływność na dysk | 100 MB/s | 150 MB/s | 200 MB/s |

Gdy hello powyżej tabeli określa maksymalną liczbę IOPS dla każdego dysku, można osiągnąć wyższy poziom wydajności przez stosowanie wielu dysków z danymi. Na przykład 64 dane, które dyski mogą być dołączony tooStandard_GS5 maszyny Wirtualnej. Jeśli każda z tych dysków o jako P30 można osiągnąć maksymalnie 80 000 IOPS. Aby uzyskać szczegółowe informacje o maksymalnej IOPS dla maszyny Wirtualnej, zobacz [rozmiarów maszyn wirtualnych systemu Linux](./sizes.md).

## <a name="create-and-attach-disks"></a>Utwórz i Dołącz dysków

przykład Witaj toocomplete w tym samouczku, musi mieć istniejącej maszyny wirtualnej. Jeśli to konieczne, to [przykładowym skrypcie](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) można utworzyć. Podczas pracy nad hello samouczek, Zastąp maszyny Wirtualnej i grupy zasobów hello nazwy w razie potrzeby.

Tworzenie początkowej konfiguracji hello o [AzureRmDiskConfig nowy](/powershell/module/azurerm.compute/new-azurermdiskconfig). Poniższy przykład Hello konfiguruje dysku, który wynosi 128 GB w rozmiarze.

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

Utwórz dysk danych hello z hello [AzureRmDisk nowy](/powershell/module/azurerm.compute/new-azurermdisk) polecenia.

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

Maszyna wirtualna hello GET, które mają tooadd hello danych dysku toowith hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) polecenia.

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

Dodaj hello danych dysku toohello konfiguracji maszyny wirtualnej z hello [AzureRmVMDataDisk Dodaj](/powershell/module/azurerm.compute/add-azurermvmdatadisk) polecenia.

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

Zaktualizuj maszynę wirtualną hello za pomocą hello [AzureRmVM aktualizacji](/powershell/module/azurerm.compute/add-azurermvmdatadisk) polecenia.

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a>Przygotowanie dysków z danymi

Po dysku maszyny wirtualnej podłączone toohello, system operacyjny hello musi toobe skonfigurowane toouse hello dysku. Witaj poniższym przykładzie przedstawiono toomanually konfiguracji hello pierwszego dysku dodane toohello maszyny Wirtualnej. Ten proces można również zautomatyzować przy użyciu hello [niestandardowe rozszerzenie skryptu](./tutorial-automate-vm-deployment.md).

### <a name="manual-configuration"></a>Konfiguracja ręczna

Utwórz połączenie RDP z maszyny wirtualnej hello. Otwieranie programu PowerShell i uruchom ten skrypt.

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a>Następne kroki

W tym samouczku przedstawiono tematy dysków maszyny Wirtualnej takich jak:

> [!div class="checklist"]
> * Dyski systemu operacyjnego i tymczasowego
> * Dyski danych
> * Standard i dysków w warstwie Premium
> * Wydajność dysku
> * Dołączanie i przygotowywania dysków z danymi

Przejdź dalej toolearn samouczka toohello dotyczące automatyzowania konfiguracji maszyny Wirtualnej.

> [!div class="nextstepaction"]
> [Automatyzowanie konfiguracji maszyny wirtualnej](./tutorial-automate-vm-deployment.md)
