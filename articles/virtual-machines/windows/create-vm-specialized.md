---
title: aaaCreate maszyny Wirtualnej systemu Windows z specjalne wirtualnego dysku twardego na platformie Azure | Dokumentacja firmy Microsoft
description: "Utwórz nową maszynę Wirtualną systemu Windows przez dołączenie specjalne dysków zarządzanych jako dysk systemu operacyjnego hello przy użyciu modelu wdrażania Menedżera zasobów hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cynthn
ms.openlocfilehash: c72c6f4fb650e2664e87cf38ec9be62f0b2209fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a>Tworzenie maszyny Wirtualnej systemu Windows z dysku specjalne

Dołączanie specjalne dysków zarządzanych jako dysk systemu operacyjnego hello przy użyciu programu Powershell, aby utworzyć nową maszynę Wirtualną. Specjalne dysku jest kopią wirtualnego dysku twardego (VHD) z istniejącej maszyny Wirtualnej utworzonej hello kont użytkowników, aplikacji i innych danych o stanie z oryginalnego maszyny Wirtualnej. 

Użycie specjalnych toocreate wirtualnego dysku twardego nowej maszyny Wirtualnej, powitalne nowej maszyny Wirtualnej zachowuje nazwy komputera hello hello oryginalna maszyna wirtualna. Inne informacje specyficzne dla komputera jest również przechowywać, a w niektórych przypadkach te informacje zduplikowane może spowodować problemy. Należy pamiętać o jakie rodzaje informacji specyficznych dla komputera aplikacje zależne od podczas kopiowania maszyny Wirtualnej.

Dostępne są dwie opcje:
* [Przekazywanie wirtualnego dysku twardego](#option-1-upload-a-specialized-vhd)
* [Skopiuj istniejącej maszyny Wirtualnej Azure](#option-2-copy-an-existing-azure-vm)

W tym temacie przedstawiono sposób toouse zarządzania dyskami. Jeśli masz wdrożenie starszych wymagający przy użyciu konta magazynu, zobacz [utworzyć Maszynę wirtualną z wirtualnego dysku twardego specjalne konta magazynu](sa-create-vm-specialized.md)

## <a name="before-you-begin"></a>Przed rozpoczęciem
Jeśli używasz programu PowerShell, upewnij się, że masz najnowszą wersję hello modułu AzureRM.Compute PowerShell hello. 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).


## <a name="option-1-upload-a-specialized-vhd"></a>Opcja 1: Przekazanie specjalne dysku VHD

Możesz przekazać powitalne wirtualnego dysku twardego z specjalistyczne maszyny Wirtualnej utworzone za pomocą wirtualizacji narzędzia lokalnych, takich jak funkcja Hyper-V lub maszyny Wirtualnej wyeksportowane z innej chmury.

### <a name="prepare-hello-vm"></a>Przygotowanie hello maszyny Wirtualnej
Jeśli planujesz toouse hello wirtualnego dysku twardego — jest toocreate nowej maszyny Wirtualnej, upewnij się, hello następujące kroki zostały zakończone. 
  
  * [Przygotowanie tooAzure tooupload wirtualnego dysku twardego Windows](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). **Nie** generalize hello maszyny Wirtualnej przy użyciu narzędzia Sysprep.
  * Usuń wszystkie narzędzia wirtualizacji gościa i agentów, które są zainstalowane na powitania maszyny Wirtualnej (np. narzędzi VMware).
  * Upewnij się, hello maszyna wirtualna jest skonfigurowana toopull jego adres IP i ustawienia DNS za pośrednictwem protokołu DHCP. To zapewnia, że ten serwer hello uzyskuje adres IP w ramach hello sieci wirtualnej podczas uruchamiania. 


### <a name="get-hello-storage-account"></a>Pobierz hello konta magazynu
Potrzebny jest magazyn konta w hello Azure toostore przekazać wirtualnego dysku twardego. Możesz użyć istniejącego konta magazynu lub Utwórz nową. 

tooshow hello dostępny magazyn kont, wpisz:

```powershell
Get-AzureRmStorageAccount
```

Jeśli chcesz toouse istniejącego konta magazynu, przejdź toohello [hello przekazywanie wirtualnego dysku twardego](#upload-the-vhd-to-your-storage-account) sekcji.

Jeśli potrzebujesz toocreate konta magazynu, wykonaj następujące kroki:

1. Potrzebna jest nazwa hello hello grupy zasobów, których można utworzyć konta magazynu hello. toofind limit wszystkie hello grupy zasobów, które są w ramach subskrypcji, wpisz:
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    Grupa zasobów o nazwie toocreate *myResourceGroup* w hello *zachodnie stany USA* regionu, wpisz:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. Utwórz konto magazynu o nazwie *mojekontomagazynu* w tej grupie zasobów za pomocą hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) polecenia cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-hello-vhd-tooyour-storage-account"></a>Przekaż konta magazynu tooyour wirtualnego dysku twardego hello 
Użyj hello [AzureRmVhd Dodaj](/powershell/module/azurerm.compute/add-azurermvhd) polecenia cmdlet tooupload hello wirtualnego dysku twardego tooa kontenera na koncie magazynu. W tym przykładzie przekazywania hello pliku *myVHD.vhd* z `"C:\Users\Public\Documents\Virtual hard disks\"` tooa konto magazynu o nazwie *mojekontomagazynu* w hello *myResourceGroup* grupy zasobów. Plik Hello jest przechowywany w kontenerze hello o nazwie *mojkontener* i będzie hello nową nazwę pliku *myUploadedVHD.vhd*.

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


W przypadku powodzenia można uzyskać odpowiedzi, która wygląda podobnie toothis:

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

W zależności od połączenia sieciowego i hello rozmiar pliku VHD, polecenie to może chwilę potrwać toocomplete

### <a name="create-a-managed-disk-from-hello-vhd"></a>Tworzenie dysku zarządzanego z hello wirtualnego dysku twardego

Tworzenie dysku zarządzanego z hello specjalizowany wirtualnego dysku twardego za pomocą konta magazynu [AzureRMDisk nowy](/powershell/module/azurerm.compute/new-azurermdisk). W tym przykładzie użyto **myOSDisk1** nazwa dysku hello naraża hello dysku w *StandardLRS* magazynu i używa *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* jako hello identyfikatora URI źródła hello wirtualnego dysku twardego.

Utwórz nową grupę zasobów dla hello nowej maszyny Wirtualnej.

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

Utwórz nowy dysk systemu operacyjnego hello z hello przekazany wirtualnego dysku twardego. 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a>Opcja 2: Kopiowanie istniejącej maszyny Wirtualnej Azure

Można utworzyć kopii maszyny wirtualnej używa zarządza dysków migawki hello maszyny Wirtualnej, a następnie za pomocą tej migawki toocreate nowy managed dysku i nowej maszyny Wirtualnej.


### <a name="take-a-snapshot-of-hello-os-disk"></a>Utwórz migawkę hello dysk systemu operacyjnego

Można wykonać migawki elementu i całej maszyny Wirtualnej (w tym wszystkie dyski) lub tylko jednego dysku. Witaj poniższej procedurze pokazano, jak hello tootake migawki tylko hello systemu operacyjnego dysk przy użyciu maszyny Wirtualnej [AzureRmSnapshot nowy](/powershell/module/azurerm.compute/new-azurermsnapshot) polecenia cmdlet. 

Ustaw niektórych parametrów. 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

Pobierz obiekt VM hello.

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
Pobierz nazwę dysku hello systemu operacyjnego.

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

Utwórz hello migawki konfigurację. 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

Witaj migawki.

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


Jeśli planujesz toouse hello migawki toocreate maszynę Wirtualną, która wymaga wydajnych toobe, użyj parametru hello `-AccountType Premium_LRS` za pomocą polecenia hello AzureRmSnapshot nowy. Parametr Hello tworzy migawkę hello, aby są przechowywane jako dysk zarządzane Premium. Dysków zarządzanych w warstwie Premium są droższe niż standardowe. Dlatego upewnij się, że naprawdę potrzebny Premium przed użyciem parametru hello.

### <a name="create-a-new-disk-from-hello-snapshot"></a>Utwórz nowy dysk z hello migawki

Tworzenie dysku zarządzanego z hello migawki za pomocą [AzureRMDisk nowy](/powershell/module/azurerm.compute/new-azurermdisk). W tym przykładzie użyto *myOSDisk* hello nazwy dysku.

Utwórz nową grupę zasobów dla hello nowej maszyny Wirtualnej.

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

Ustaw nazwę dysku hello systemu operacyjnego. 

```powershell
$osDiskName = 'myOsDisk'
```

Utwórz hello dysków zarządzanych.

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-hello-new-vm"></a>Utwórz hello nowej maszyny Wirtualnej 

Tworzenie sieci i innych toobe zasoby maszyn wirtualnych używanych przez hello nowej maszyny Wirtualnej.

### <a name="create-hello-subnet-and-vnet"></a>Tworzenie hello podsieci i sieci wirtualnej

Tworzenie sieci wirtualnej hello i podsieci hello [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md).

Utwórz podsieć hello. W tym przykładzie tworzy podsieć o nazwie **mySubNet**, w grupie zasobów hello **myDestinationResourceGroup**, i ustawia prefiks adresu podsieci hello zbyt**10.0.0.0/24**.
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

Utwórz sieć wirtualną hello. W tym przykładzie zestawy hello toobe nazwa sieci wirtualnej **myVnetName**, zbyt hello lokalizacji**zachodnie stany USA**, i hello prefiks adresu sieci wirtualnej hello zbyt**10.0.0.0/16**. 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Tworzenie grupy zabezpieczeń sieci hello i reguły protokołu RDP
toobe stanie toolog w tooyour maszyny Wirtualnej przy użyciu protokołu RDP, należy toohave regułę zabezpieczeń, która udziela dostępu RDP do portu 3389. Ponieważ hello wirtualnego dysku twardego dla nowej maszyny Wirtualnej został utworzony na podstawie istniejącej maszyny Wirtualnej specjalne hello, można użyć konta ze źródłowej maszyny wirtualnej hello protokołu RDP.

W tym przykładzie zestawy hello Nazwa grupy NSG zbyt**myNsg** i hello RDP Nazwa reguły zbyt**myRdpRule**.

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

Aby uzyskać więcej informacji na temat punktów końcowych i reguły NSG, zobacz [otwierania portów tooa maszyny Wirtualnej na platformie Azure przy użyciu programu PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="create-a-public-ip-address-and-nic"></a>Tworzenie publicznego adresu IP i karty Sieciowej
tooenable komunikację z maszyną wirtualną hello w sieci wirtualnej hello, należy [publicznego adresu IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) i interfejsu sieciowego.

Utwórz hello publicznego adresu IP. W tym przykładzie ustawiono zbyt hello nazwa publicznego adresu IP**myIP**.
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

Utwórz hello karty sieciowej. W tym przykładzie ustawiono zbyt nazwy kart hello**myNicName**.
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-hello-vm-name-and-size"></a>Nazwa maszyny Wirtualnej hello zestawu i rozmiaru

W tym przykładzie zestawy hello nazwę maszyny Wirtualnej za*myVM* i hello wirtualna jego rozmiar za*Standard_A2*.

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a>Dodaj hello karty Sieciowej
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-hello-os-disk"></a>Dodaj dysk hello systemu operacyjnego 

Dodaj hello systemu operacyjnego dysku toohello konfiguracji przy użyciu [AzureRmVMOSDisk zestawu](/powershell/module/azurerm.compute/set-azurermvmosdisk). W tym przykładzie hello rozmiar dysku hello zbyt*128 GB* i dołącza hello dysków zarządzanych jako *Windows* dysku systemu operacyjnego.
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-hello-vm"></a>Ukończyć powitalnych maszyny Wirtualnej 

Utwórz maszynę Wirtualną przy użyciu hello [AzureRMVM nowy](/powershell/module/azurerm.compute/new-azurermvm)hello konfiguracje, które właśnie utworzyliśmy.

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

Jeśli to polecenie zakończyło się pomyślnie, zostanie wyświetlone dane wyjściowe w następujący sposób:

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a>Sprawdź hello, że maszyna wirtualna została utworzona
Powinny pojawić się hello nowo utworzona maszyna wirtualna w hello [portalu Azure](https://portal.azure.com)w obszarze **Przeglądaj** > **maszyn wirtualnych**, lub za pomocą hello następującego środowiska PowerShell polecenia:

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a>Następne kroki
toosign w tooyour nowej maszyny wirtualnej, przeglądania toohello maszyny Wirtualnej w hello [portal](https://portal.azure.com), kliknij przycisk **Connect**i hello Otwórz plik RDP pulpitu zdalnego. Użyj poświadczeń konta hello z oryginalnego toosign maszyny wirtualnej w tooyour nowej maszyny wirtualnej. Aby uzyskać więcej informacji, zobacz [jak dziennika na tooan wirtualnej platformy Azure i tooconnect maszyny, systemem operacyjnym Windows](connect-logon.md).

