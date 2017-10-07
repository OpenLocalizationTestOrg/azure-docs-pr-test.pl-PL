---
title: "aaaCreate niezarządzane obraz uogólniony maszyny wirtualnej na platformie Azure | Dokumentacja firmy Microsoft"
description: "Utwórz obraz unmanged uogólniony toocreate toouse maszyny Wirtualnej systemu Windows wiele kopii maszyny wirtualnej na platformie Azure."
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
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: b8a044d20313efa6dd9b9757e61154f922134476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-unmanaged-vm-image-from-an-azure-vm"></a>Jak obraz toocreate niezarządzane maszyny Wirtualnej z maszyny Wirtualnej platformy Azure

W tym artykule omówiono używanie kont magazynu. Zalecane jest użycie dysków zarządzanych i zarządzanych obrazów zamiast konta magazynu. Aby uzyskać więcej informacji, zobacz [Przechwyć obraz zarządzanych uogólniony maszyny wirtualnej na platformie Azure](capture-image-resource.md).

W tym artykule opisano sposób toouse programu Azure PowerShell toocreate obraz uogólniony maszyny Wirtualnej platformy Azure przy użyciu konta magazynu. Następnie można toocreate obraz powitania inną maszynę Wirtualną. Obraz powitania obejmuje hello dysk systemu operacyjnego i dysków danych hello, które są dołączone toohello maszyny wirtualnej. Obraz powitania nie zawiera zasobów sieci wirtualnej hello, więc należy tooset tych zasobów, podczas tworzenia nowej maszyny Wirtualnej hello. 

## <a name="prerequisites"></a>Wymagania wstępne
Wymagana wersja programu Azure PowerShell toohave 1.0.x lub nowszej. Jeśli jeszcze nie zainstalowano programu PowerShell, przeczytaj [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) kroki instalacji.

## <a name="generalize-hello-vm"></a>Generalize hello maszyny Wirtualnej 
W tej sekcji opisano sposób toogeneralize maszyny wirtualnej systemu Windows do użycia jako obraz. Uogólnianie maszyny Wirtualnej powoduje usunięcie wszystkich informacji osobowych konta, między innymi i przygotowuje toobe maszyny hello użyty jako obraz. Aby uzyskać więcej informacji o narzędziu Sysprep, zobacz [jak tooUse Sysprep: wprowadzenie](http://technet.microsoft.com/library/bb457073.aspx).

Upewnij się, że hello ról serwera uruchomionych na maszynie hello są obsługiwane przez program Sysprep. Aby uzyskać więcej informacji, zobacz [Obsługa programu Sysprep dla ról serwera](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> Podczas przekazywania tooAzure Twojego dysku VHD na powitania po raz pierwszy, upewnij się, masz [przygotować maszyny Wirtualnej](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) przed uruchomieniem programu Sysprep. 
> 
> 

Można również generalize maszyny Wirtualnej systemu Linux przy użyciu `sudo waagent -deprovision+user` , a następnie użyj programu PowerShell toocapture hello maszyny Wirtualnej. Aby dowiedzieć się, jak przy użyciu hello CLI toocapture maszyny Wirtualnej, zobacz [jak toogeneralize i przechwycenia maszyny wirtualnej systemu Linux przy użyciu interfejsu wiersza polecenia Azure hello ](../linux/capture-image.md).


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

## <a name="log-in-tooazure-powershell"></a>Zaloguj się za tooAzure programu PowerShell
1. Otwórz program Azure PowerShell i zaloguj się na tooyour konto platformy Azure.
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    Zostanie otwarte okno podręczne dla tooenter możesz poświadczenia konta Azure.
2. Uzyskanie subskrypcji hello identyfikatorów subskrypcji dostępne.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Ustaw poprawną subskrypcję hello przy użyciu identyfikatora hello subskrypcji.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-hello-vm-and-set-hello-state-toogeneralized"></a>Cofnięcie przydziału hello maszyny Wirtualnej i ustaw hello toogeneralized stanu
1. Cofnięcie przydziału hello zasobów maszyny Wirtualnej.
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    Witaj *stan* dla hello maszyny Wirtualnej w hello Azure portal zmieni się z **zatrzymane** za**zatrzymane (cofnięciu przydziału)**.
2. Ustaw stan hello hello maszyny wirtualnej za**Uogólniono**. 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. Sprawdź stan hello hello maszyny Wirtualnej. Witaj **OSState/uogólniony** sekcji hello maszyny Wirtualnej powinny mieć hello **DisplayStatus** ustawić także**uogólniona maszyna wirtualna**.  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-hello-image"></a>Utworzyć obraz powitania

Tworzenie obrazu niezarządzane maszyny wirtualnej w hello docelowy kontener magazynu przy użyciu tego polecenia. Witaj obrazu jest tworzony w hello same konta magazynu, ponieważ hello oryginalna maszyna wirtualna. Witaj `-Path` parametr zapisuje kopię szablonu JSON hello na komputerze lokalnym tooyour hello źródłowej maszyny Wirtualnej. Witaj `-DestinationContainerName` parametru jest nazwa hello kontenera hello mają toohold obrazów. Jeśli hello kontener nie istnieje, jest tworzony automatycznie.
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
Możesz pobrać ze strony szablonu pliku JSON hello hello adres URL obrazu. Przejdź toohello **zasobów** > **storageProfile** > **osDisk** > **obrazu**  >  **uri** sekcji hello pełną ścieżkę obrazu. adres URL obrazu, hello Hello wygląda następująco: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.
   
Można również sprawdzić hello identyfikatora URI w portalu hello. Obraz powitania jest skopiowany tooa kontener o nazwie **systemu** na koncie magazynu. 

## <a name="create-a-vm-from-hello-image"></a>Utwórz maszynę Wirtualną z obrazu hello

Teraz możesz utworzyć przynajmniej jednej maszyny wirtualnej z obrazu niezarządzane hello.

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
Hello następujące PowerShell kończy hello konfiguracje maszyny wirtualnej i używa niezarządzanej obrazu jako źródła hello hello nowej instalacji.

</br>

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

### <a name="verify-that-hello-vm-was-created"></a>Sprawdź hello, że maszyna wirtualna została utworzona
Po zakończeniu powinien zostać wyświetlony hello nowo utworzony maszyny Wirtualnej w hello [portalu Azure](https://portal.azure.com) w obszarze **Przeglądaj** > **maszyn wirtualnych**, lub za pomocą następujących hello Polecenia programu PowerShell:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Następne kroki
toomanage nowej maszyny wirtualnej przy użyciu programu Azure PowerShell, zobacz [zarządzania maszynami wirtualnymi przy użyciu usługi Azure Resource Manager i programu PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


