---
title: "aaaMigrate tooan klasyczne maszyny Wirtualnej VM dysku zarządzanego ARM | Dokumentacja firmy Microsoft"
description: "Migrację jednej maszyny Wirtualnej platformy Azure z hello wdrażania klasycznego modelu tooManaged dysków w modelu wdrażania usługi Resource Manager hello."
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
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: d8c4b9431f5dd8a071fcbc2ee36581a33f76ba62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manually-migrate-a-classic-vm-tooa-new-arm-managed-disk-vm-from-hello-vhd"></a>Ręcznej migracji tooa klasycznego wirtualna nowej ARM zarządzane dysku maszyny Wirtualnej z hello wirtualnego dysku twardego 


Ta sekcja pomoże toomigrate możesz istniejących maszyn wirtualnych platformy Azure z hello klasycznego modelu wdrażania zbyt[dysków zarządzanych](managed-disks-overview.md) w modelu wdrażania usługi Resource Manager hello.


## <a name="plan-for-hello-migration-toomanaged-disks"></a>Planowanie migracji hello tooManaged dysków

Ta sekcja pomoże toomake hello najlepszych decyzji w typach maszyny Wirtualnej i dysku.


### <a name="location"></a>Lokalizacja

Wybierz lokalizację, w której są dostępne dyski zarządzanych Azure. W przypadku migracji dysków zarządzanych tooPremium, upewnij się również magazyn w warstwie Premium jest dostępna w regionie hello planowanego toomigrate do. Zobacz [byRegion usług Azure](https://azure.microsoft.com/regions/#services) aktualne informacje o dostępnych lokalizacji.

### <a name="vm-sizes"></a>Rozmiary maszyn wirtualnych

W przypadku migracji dysków zarządzanych tooPremium masz tooupdate rozmiar hello hello wirtualna tooPremium rozmiar możliwością magazynu dostępnych w regionie hello, w którym znajduje się maszyna wirtualna. Przejrzyj hello rozmiarów maszyn wirtualnych, które są funkcją Magazyn w warstwie Premium. specyfikacje rozmiaru maszyny Wirtualnej Azure Hello są wymienione w [rozmiary maszyn wirtualnych](sizes.md).
Przejrzyj hello charakterystyki wydajności maszyn wirtualnych, które pracować z magazyn w warstwie Premium i wybierz polecenie hello najbardziej odpowiedni rozmiar maszyny Wirtualnej najlepiej pasujące do obciążenia. Upewnij się, czy Brak dostępnej wystarczającą przepustowość na ruchu dysku hello toodrive maszyny Wirtualnej.

### <a name="disk-sizes"></a>Rozmiary dysków

**Dysków zarządzanych w warstwie Premium**

Istnieje siedem typów dysków zarządzane premium, które mogą być używane z maszyny Wirtualnej i każdy ma określonych IOPs i przepływność limity. W przypadku wybrania hello Premium typ dysku dla maszyny Wirtualnej na podstawie hello potrzeb aplikacji pod względem wydajności, wydajności, skalowalności i ładuje szczytu, należy wziąć pod uwagę te limity.

| Typ dysków Premium  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Rozmiar dysku           | 128 GB| 512 GB| 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| Liczba operacji wejścia/wyjścia na sekundę na dysk       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Przepływność na dysk | 25 MB na sekundę  | 50 MB / s  | 100 MB na sekundę | 150 MB na sekundę | 200 MB / s | 250 MB na sekundę | 250 MB na sekundę | 

**Dyski standardowe zarządzanych**

Istnieje siedem typów zarządzane standardowych dysków, które mogą być używane z maszyny Wirtualnej. Każdej z nich ma inną wydajności, ale ma tego samego IOPS i limity przepustowości. Wybierz typ hello dyski standardowe zarządzane na podstawie hello pojemności potrzeb aplikacji.

| Typ dysku standardowego  | S4               | S6               | S10              | S20              | S30              | S40              | S50              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| Rozmiar dysku           | 30 GB            | 64 GB            | 128 GB           | 512 GB           | 1024 GB (1 TB)   | 2048 GB (2TB)    | 4095 GB (4 TB)   | 
| Liczba operacji wejścia/wyjścia na sekundę na dysk       | 500              | 500              | 500              | 500              | 500              | 500             | 500              | 
| Przepływność na dysk | 60 MB na sekundę | 60 MB na sekundę | 60 MB na sekundę | 60 MB na sekundę | 60 MB na sekundę | 60 MB na sekundę | 60 MB na sekundę | 


### <a name="disk-caching-policy"></a>Dyskowej pamięci podręcznej zasad 

**Dysków zarządzanych w warstwie Premium**

Domyślnie jest dyskowej pamięci podręcznej zasad *tylko do odczytu* dla wszystkich hello dysków danych w warstwie Premium i *odczytu i zapisu* dla dysku systemu operacyjnego Premium hello dołączony toohello maszyny Wirtualnej. To ustawienie konfiguracji jest zalecane tooachieve hello optymalnej wydajności dla aplikacji systemu IOs. W przypadku dysków ciężki zapisu lub w trybie tylko do zapisu danych (takich jak pliki dziennika programu SQL Server) Wyłącz buforowanie dysku, dzięki czemu można osiągnąć lepszą wydajność aplikacji.

### <a name="pricing"></a>Cennik

Przejrzyj hello [ceny dysków zarządzanych](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Cen dysków zarządzanych w warstwie Premium jest taka sama jak hello niezarządzane dysków Premium. Ale ceny dyski standardowe zarządzanych jest inny niż dyski standardowe niezarządzane.


## <a name="checklist"></a>Lista kontrolna

1.  W przypadku migracji dysków zarządzanych tooPremium, upewnij się, że jest dostępna w regionie hello, które w przypadku migracji do.

2.  Zdecyduj, hello nowej serii maszyn wirtualnych, które będą używane. Jeśli przeprowadzasz migrację dysków zarządzanych tooPremium powinno być funkcją Magazyn w warstwie Premium.

3.  Zdecyduj, hello dokładny rozmiar maszyny Wirtualnej, który będzie używany, które są dostępne w regionie hello, które w przypadku migracji do. Rozmiar maszyny Wirtualnej musi toobe toosupport wystarczająco duży hello liczba dysków danych, do których masz. Na przykład jeśli masz cztery dyski danych hello maszyna wirtualna musi mieć co najmniej dwa rdzenie. Należy również rozważyć przetwarzania zasilania, pamięci i musi przepustowości sieci.

4.  Ma hello wirtualna szczegóły bieżącej przydatną tym hello listę dysków i odpowiednie obiekty BLOB dysków VHD.

Przygotowanie aplikacji dla przestoju. toodo czystą migracji należy toostop przetwarzania hello w bieżącym systemie hello. Następnie możesz pobrać go tooconsistent stanu, które można migrować toohello na nowej platformie. Czas trwania przestoju zależy od hello ilości danych w hello toomigrate dysków.


## <a name="migrate-hello-vm"></a>Migrowanie hello maszyny Wirtualnej

Przygotowanie aplikacji dla przestoju. toodo czystą migracji należy toostop przetwarzania hello w bieżącym systemie hello. Następnie możesz pobrać go tooconsistent stanu, które można migrować toohello na nowej platformie. Czas trwania przestoju zależy od hello ilości danych w hello toomigrate dysków.


1.  Najpierw należy ustawić hello typowe parametry:

    ```powershell
    $resourceGroupName = 'yourResourceGroupName'
    
    $location = 'your location' 
    
    $virtualNetworkName = 'yourExistingVirtualNetworkName'
    
    $virtualMachineName = 'yourVMName'
    
    $virtualMachineSize = 'Standard_DS3'
    
    $adminUserName = "youradminusername"
    
    $adminPassword = "yourpassword" | ConvertTo-SecureString -AsPlainText -Force
    
    $imageName = 'yourImageName'
    
    $osVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd'
    
    $dataVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk1.vhd'
    
    $dataDiskName = 'dataDisk1'
    ```

2.  Tworzenie zarządzanego dysku systemu operacyjnego przy użyciu hello wirtualnego dysku twardego z hello klasyczne maszyny Wirtualnej.

    Upewnij się, że masz pod warunkiem hello ukończyć URI hello parametru toohello $osVhdUri wirtualnego dysku twardego systemu operacyjnego. Wprowadź też **- AccountType** jako **PremiumLRS** lub **StandardLRS** na podstawie typu dysków (Premium lub Standard) w przypadku migracji do.

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  Dołącz toohello dysku systemu operacyjnego hello nowej maszyny Wirtualnej.

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  Utwórz dysk danych zarządzanych z pliku VHD danych hello i dodaj go toohello nowej maszyny Wirtualnej.

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  Utwórz hello nowej maszyny Wirtualnej przez ustawienie publicznego adresu IP, sieci wirtualnej i karty sieciowej.

    ```powershell
    $publicIp = New-AzureRmPublicIpAddress -Name ($VirtualMachineName.ToLower()+'_ip') '
    -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
    
    $vnet = Get-AzureRmVirtualNetwork -Name $virtualNetworkName -ResourceGroupName $resourceGroupName
    
    $nic = New-AzureRmNetworkInterface -Name ($VirtualMachineName.ToLower()+'_nic') '
    -ResourceGroupName $resourceGroupName -Location $location -SubnetId $vnet.Subnets[0].Id '
    -PublicIpAddressId $publicIp.Id
    
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $nic.Id
    
    New-AzureRmVM -VM $VirtualMachine -ResourceGroupName $resourceGroupName -Location $location
    ```

> [!NOTE]
>Może być konieczne toosupport dodatkowe kroki aplikacji, która jest nie obejmuje się w tym przewodniku.
>
>

## <a name="next-steps"></a>Następne kroki

- Połącz toohello maszyny wirtualnej. Aby uzyskać instrukcje, zobacz [jak dziennika na tooan wirtualnej platformy Azure i tooconnect maszyny, systemem operacyjnym Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

