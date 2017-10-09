---
title: aaaUpload toocreate wirtualnego dysku twardego generalize wiele maszyn wirtualnych na platformie Azure | Dokumentacja firmy Microsoft
description: "Przekaż uogólniony wirtualny dysk twardy tooan magazynu Azure konta toocreate toouse maszyny Wirtualnej systemu Windows, z modelu wdrażania usługi Resource Manager hello."
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
ms.date: 05/18/2017
ms.author: cynthn
ms.openlocfilehash: aa1af2a0acf81685e62853de71afa51e819cb696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-tooazure-toocreate-a-new-vm"></a>Przekaż uogólniony wirtualny dysk twardy tooAzure toocreate nowej maszyny Wirtualnej

W tym temacie omówiono przekazywania konta magazynu tooa uogólniony dysk niezarządzane, a następnie utworzenie nowej maszyny Wirtualnej przy użyciu dysku hello przekazany. Obraz uogólniony wirtualny dysk twardy ma wszystkie informacje osobiste Konto usunięte za pomocą programu Sysprep. 

Jeśli chcesz toocreate Maszynę wirtualną z wirtualnego dysku twardego specjalne na koncie magazynu, zobacz [tworzenie maszyny Wirtualnej z dysku VHD specjalne](sa-create-vm-specialized.md).

W tym temacie omówiono używanie kont magazynu, ale zaleca się, że klienci przenoszenie dysków zarządzanych toousing zamiast tego. Na dyskach zarządzanych pełny przewodnik sposobu tooprepare, przekazywanie i Utwórz nowe przy użyciu maszyny Wirtualnej, zobacz [Utwórz nową maszynę Wirtualną z ogólnych tooAzure przekazany wirtualny dysk twardy za pomocą dysków zarządzanych](upload-generalized-managed.md).



## <a name="prepare-hello-vm"></a>Przygotowanie hello maszyny Wirtualnej

Uogólniony wirtualny dysk twardy ma wszystkie informacje osobiste Konto usunięte za pomocą programu Sysprep. Jeśli planujesz hello toouse toocreate obrazu wirtualnego dysku twardego nowych maszyn wirtualnych z, wykonaj następujące czynności:
  
  * [Przygotowanie tooAzure tooupload wirtualnego dysku twardego Windows](prepare-for-upload-vhd-image.md). 
  * Hello maszyny wirtualnej za pomocą programu Sysprep do uogólnienia

### <a name="generalize-a-windows-virtual-machine-using-sysprep"></a>Maszyny wirtualnej systemu Windows za pomocą programu Sysprep do uogólnienia
W tej sekcji opisano sposób toogeneralize maszyny wirtualnej systemu Windows do użycia jako obraz. Program Sysprep usuwa wszystkie informacje osobiste konto, między innymi i przygotowuje toobe maszyny hello użyty jako obraz. Aby uzyskać więcej informacji o narzędziu Sysprep, zobacz [jak tooUse Sysprep: wprowadzenie](http://technet.microsoft.com/library/bb457073.aspx).

Upewnij się, że hello ról serwera uruchomionych na maszynie hello są obsługiwane przez program Sysprep. Aby uzyskać więcej informacji, zobacz [Obsługa programu Sysprep dla ról serwera](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> Jeśli korzystasz z programu Sysprep przed przekazaniem tooAzure Twojego dysku VHD na powitania po raz pierwszy, upewnij się, masz [przygotować maszyny Wirtualnej](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) przed uruchomieniem programu Sysprep. 
> 
> 

1. Zaloguj się toohello maszyny wirtualnej systemu Windows.
2. Otwórz okno wiersza polecenia hello jako administrator. Zmień katalog hello zbyt**%windir%\system32\sysprep**, a następnie uruchom `sysprep.exe`.
3. W hello **narzędzie przygotowania systemu** okno dialogowe, wybierz opcję **wprowadź systemu Out-of-Box Experience (OOBE)**i upewnij się, że hello **Generalize** pole wyboru jest zaznaczone.
4. W **opcje zamykania**, wybierz pozycję **zamknięcia**.
5. Kliknij przycisk **OK**.
   
    ![Uruchom program Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. Po zakończeniu działania programu Sysprep, zamyka hello maszyny wirtualnej. 

> [!IMPORTANT]
> Nie uruchamiaj ponownie hello maszyny Wirtualnej, dopóki nie są gotowe, przesyłania tooAzure wirtualnego dysku twardego hello lub Tworzenie obrazu z hello maszyny Wirtualnej. Jeśli hello wirtualna przypadkowo pobiera ponownie uruchomione, uruchom Sysprep toogeneralize go ponownie.
> 
> 


## <a name="upload-hello-vhd"></a>Przekaż hello wirtualnego dysku twardego

Przekaż hello wirtualnego dysku twardego tooan konta magazynu Azure.

### <a name="log-in-tooazure"></a>Zaloguj się za tooAzure
Jeśli nie masz jeszcze programu PowerShell w wersji 1.4 lub nowszy zainstalowany, przeczytaj [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

1. Otwórz program Azure PowerShell i zaloguj się na tooyour konto platformy Azure. Zostanie otwarte okno podręczne dla tooenter możesz poświadczenia konta Azure.
   
    ```powershell
    Login-AzureRmAccount
    ```
2. Uzyskanie subskrypcji hello identyfikatorów subskrypcji dostępne.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Ustaw poprawną subskrypcję hello przy użyciu identyfikatora hello subskrypcji. Zastąp `<subscriptionID>` o identyfikatorze hello hello Popraw subskrypcji.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

### <a name="get-hello-storage-account"></a>Pobierz hello konta magazynu
Musisz mieć konto magazynu, w obrazie maszyny Wirtualnej Azure toostore hello przekazany. Możesz użyć istniejącego konta magazynu lub Utwórz nową. 

tooshow hello dostępny magazyn kont, wpisz:

```powershell
Get-AzureRmStorageAccount
```

Jeśli chcesz toouse istniejącego konta magazynu, przejdź toohello [obrazu maszyny Wirtualnej hello przekazywania](#upload-the-vm-vhd-to-your-storage-account) sekcji.

Jeśli potrzebujesz toocreate konta magazynu, wykonaj następujące kroki:

1. Potrzebna jest nazwa hello hello grupy zasobów, których można utworzyć konta magazynu hello. toofind limit wszystkie hello grupy zasobów, które są w ramach subskrypcji, wpisz:
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    Grupa zasobów o nazwie toocreate **myResourceGroup** w hello **zachodnie stany USA** regionu, wpisz:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. Utwórz konto magazynu o nazwie **mojekontomagazynu** w tej grupie zasobów za pomocą hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) polecenia cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
 
### <a name="start-hello-upload"></a>Rozpocznij przekazywanie hello 

Użyj hello [AzureRmVhd Dodaj](/powershell/module/azurerm.compute/add-azurermvhd) polecenia cmdlet tooupload hello obrazu tooa kontenera na koncie magazynu. W tym przykładzie przekazywania hello pliku **myVHD.vhd** z `"C:\Users\Public\Documents\Virtual hard disks\"` tooa konto magazynu o nazwie **mojekontomagazynu** w hello **myResourceGroup** grupy zasobów. Plik Hello zostaną umieszczone w hello kontener o nazwie **mojkontener** i będzie hello nową nazwę pliku **myUploadedVHD.vhd**.

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
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

W zależności od połączenia sieciowego i hello rozmiar pliku VHD, polecenie to może chwilę potrwać toocomplete.


## <a name="create-a-new-vm"></a>Tworzenie nowej maszyny Wirtualnej 

Możesz teraz hello Użyj przekazać toocreate wirtualnego dysku twardego nowej maszyny Wirtualnej. 

### <a name="set-hello-uri-of-hello-vhd"></a>Ustaw hello URI hello wirtualnego dysku twardego

Hello identyfikatora URI dla toouse wirtualnego dysku twardego hello jest w formacie hello: https://**mojekontomagazynu**.blob.core.windows.net/**mojkontener**/**MyVhdName**VHD. W tym przykładzie hello wirtualnego dysku twardego o nazwie **myVHD** jest na koncie magazynu hello **mojekontomagazynu** w kontenerze hello **mojkontener**.

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a>Tworzenie sieci wirtualnej
Tworzenie sieci wirtualnej hello i podsieci hello [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md).

1. Utwórz podsieć hello. Witaj poniższy przykład tworzy podsieć o nazwie **mySubnet** w grupie zasobów hello **myResourceGroup** z prefiksu adresu hello **10.0.0.0/24**.  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Utwórz sieć wirtualną hello. Witaj poniższy przykład tworzy sieć wirtualną o nazwie **myVnet** w hello **zachodnie stany USA** lokalizacji z prefiksu adresu hello **10.0.0.0/16**.  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a>Tworzenie publicznego adresu IP adres i interfejsu sieciowego
tooenable komunikację z maszyną wirtualną hello w sieci wirtualnej hello, należy [publicznego adresu IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) i interfejsu sieciowego.

1. Utwórz publiczny adres IP. W tym przykładzie jest tworzony publiczny adres IP o nazwie **myPip**. 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Utwórz hello karty sieciowej. W tym przykładzie jest tworzony karty Sieciowej o nazwie **myNic**. 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Tworzenie grupy zabezpieczeń sieci hello i reguły protokołu RDP
toobe stanie toolog w tooyour maszyny Wirtualnej przy użyciu protokołu RDP, należy toohave regułę zabezpieczeń, która udziela dostępu RDP do portu 3389. 

W tym przykładzie tworzy grupy NSG o nazwie **myNsg** zawierający regułę o nazwie **myRdpRule** za pośrednictwem portu 3389 która zezwala na ruch RDP. Aby uzyskać więcej informacji na temat grup NSG, zobacz [otwierania portów tooa maszyny Wirtualnej na platformie Azure przy użyciu programu PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a>Utwórz zmienną hello sieci wirtualnej
Utwórz zmienną ukończyć powitalnych sieci wirtualnej. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a>Utwórz hello maszyny Wirtualnej
Witaj następujący skrypt programu PowerShell pokazuje sposób tooset hello konfiguracje maszyny wirtualnej i użyj hello przekazać obraz maszyny Wirtualnej jako źródło hello hello nowa instalacja.



```powershell
# Enter a new user name and password toouse as hello local administrator account 
    # for remotely accessing hello VM.
    $cred = Get-Credential

    # Name of hello storage account where hello VHD is located. This example sets hello 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of hello virtual machine. This example sets hello VM name as "myVM".
    $vmName = "myVM"

    # Size of hello virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See hello VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for hello VM. This examples sets hello computer name as "myComputer".
    $computerName = "myComputer"

    # Name of hello disk that holds hello OS. This example sets hello 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets hello SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get hello storage account where hello uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set hello VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set hello Windows operating system configuration and add hello NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create hello OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure hello OS disk toobe created from hello existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create hello new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

## <a name="verify-that-hello-vm-was-created"></a>Sprawdź hello, że maszyna wirtualna została utworzona
Po zakończeniu powinien zostać wyświetlony hello nowo utworzony maszyny Wirtualnej w hello [portalu Azure](https://portal.azure.com) w obszarze **Przeglądaj** > **maszyn wirtualnych**, lub za pomocą następujących hello Polecenia programu PowerShell:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Następne kroki
toomanage nowej maszyny wirtualnej przy użyciu programu Azure PowerShell, zobacz [zarządzania maszynami wirtualnymi przy użyciu usługi Azure Resource Manager i programu PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


