---
title: "aaaCreate niestandardowych obrazów maszyn wirtualnych z hello Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Samouczek — Tworzenie niestandardowego obrazu maszyny Wirtualnej przy użyciu hello Azure PowerShell."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 3a759fe1b7e7b72f531399b0f4a99e341713c6a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a>Tworzenie niestandardowego obrazu maszyny Wirtualnej platformy Azure przy użyciu programu PowerShell

Niestandardowe obrazy są takie jak obrazy marketplace, ale można je utworzyć samodzielnie. Niestandardowe obrazy mogą być używane toobootstrap konfiguracje, takie jak wstępnego ładowania aplikacji, konfiguracji aplikacji i inne konfiguracje systemu operacyjnego. W tym samouczku utworzysz własnego niestandardowego obrazu maszyny wirtualnej platformy Azure. Omawiane kwestie:

> [!div class="checklist"]
> * Narzędzie Sysprep i generalize maszyny wirtualne
> * Tworzenie obrazu niestandardowego
> * Utwórz maszynę Wirtualną z obrazu niestandardowego
> * Wyświetlanie listy wszystkich obrazów hello w ramach subskrypcji
> * Usuń obraz

Ten samouczek wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej. Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji. Jeśli potrzebujesz tooupgrade, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="before-you-begin"></a>Przed rozpoczęciem

Poniższe kroki Hello szczegółowo tootake istniejącej maszyny Wirtualnej i włącz go do wielokrotnego użytku niestandardowego obrazu, który służy toocreate nowych wystąpień maszyny Wirtualnej.

przykład Witaj toocomplete w tym samouczku, musi mieć istniejącej maszyny wirtualnej. Jeśli to konieczne, to [przykładowym skrypcie](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) można utworzyć. Podczas pracy nad hello samouczek, Zastąp maszyny Wirtualnej i grupy zasobów hello nazwy w razie potrzeby.

## <a name="prepare-vm"></a>Przygotowywanie maszyny Wirtualnej

toocreate obrazu maszyny wirtualnej, należy tooprepare hello maszyny Wirtualnej przez uogólnianie hello maszyny Wirtualnej, dealokowanie, a następnie oznaczenie hello źródłowej maszyny Wirtualnej, ponieważ uogólniony na platformie Azure.

### <a name="generalize-hello-windows-vm-using-sysprep"></a>Generalize hello maszyny Wirtualnej systemu Windows za pomocą programu Sysprep

Program Sysprep usuwa wszystkie informacje osobiste konto, między innymi i przygotowuje toobe maszyny hello użyty jako obraz. Aby uzyskać więcej informacji o narzędziu Sysprep, zobacz [jak tooUse Sysprep: wprowadzenie](http://technet.microsoft.com/library/bb457073.aspx).


1. Połącz toohello maszyny wirtualnej.
2. Otwórz okno wiersza polecenia hello jako administrator. Zmień katalog hello zbyt*%windir%\system32\sysprep*, a następnie uruchom *sysprep.exe*.
3. W hello **narzędzie przygotowania systemu** okno dialogowe, wybierz opcję *wprowadź systemu Out-of-Box Experience (OOBE)*i upewnij się, że hello *Generalize* pole wyboru jest zaznaczone.
4. W **opcje zamykania**, wybierz pozycję *zamknięcia* , a następnie kliknij przycisk **OK**.
5. Po zakończeniu działania programu Sysprep, zamyka hello maszyny wirtualnej. **Nie uruchamiaj ponownie hello wirtualna**.

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a>Cofnięcie przydziału i oznacz hello maszyny Wirtualnej, ponieważ uogólniony

toocreate obraz powitania maszyny Wirtualnej musi toobe alokację i oznaczone jako uogólniony na platformie Azure.

Deallocated hello maszynę Wirtualną przy użyciu [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

Ustaw stan hello hello maszyny wirtualnej za`-Generalized` przy użyciu [AzureRmVm zestawu](/powershell/module/azurerm.compute/set-azurermvm). 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-hello-image"></a>Utworzyć obraz powitania

Teraz można utworzyć obraz powitania maszyny Wirtualnej za pomocą [AzureRmImageConfig nowy](/powershell/module/azurerm.compute/new-azurermimageconfig) i [AzureRmImage nowy](/powershell/module/azurerm.compute/new-azurermimage). Witaj poniższy przykład tworzy obraz o nazwie *myImage* z maszyny Wirtualnej o nazwie *myVM*.

Pobierz hello maszyny wirtualnej. 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

Utwórz konfigurację obraz powitania.

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

Utwórz obraz powitania.

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-hello-image"></a>Tworzenie maszyn wirtualnych z hello obrazu

Teraz, gdy masz obrazu można utworzyć jeden lub więcej nowych maszyn wirtualnych z hello obrazu. Tworzenie maszyny Wirtualnej z obrazu niestandardowego jest bardzo podobne toocreating Maszynę wirtualną przy użyciu obrazu z witryny Marketplace. Korzystając z obrazu z witryny Marketplace, masz tooinformation o obraz powitania, dostawca obrazu, oferty, jednostki SKU i wersji. Z niestandardowego obrazu wystarczy tooprovide hello identyfikator zasobu obrazu niestandardowego hello. 

W hello następującego skryptu, możemy utworzyć zmienną *$image* toostore informacji o korzystaniu z hello niestandardowego obrazu [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) , a następnie używamy [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)i podaj identyfikator hello przy użyciu hello *$image* zmiennej właśnie utworzyliśmy. 

Witaj skrypt tworzy Maszynę wirtualną o nazwie *myVMfromImage* z naszych obraz niestandardowy w nowej grupy zasobów o nazwie *myResourceGroupFromImage* w hello *zachodnie stany USA* lokalizacji.


```powershell
$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

New-AzureRmResourceGroup -Name myResourceGroupFromImage -Location EastUS

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name "mypublicdns$(Get-Random)" `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4

  $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

  $nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$vmConfig = New-AzureRmVMConfig `
    -VMName myVMfromImage `
    -VMSize Standard_D1 | Set-AzureRmVMOperatingSystem -Windows `
        -ComputerName myComputer `
        -Credential $cred 

# Here is where we create a variable toostore information about hello image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want toocreate hello VM from and image and provide hello image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a>Zarządzanie obrazami 

Oto kilka przykładów typowych zadań zarządzania dla obrazu i w jaki sposób toocomplete ich przy użyciu programu PowerShell.

Wyświetl listę wszystkich obrazów według nazwy.

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

Usuń obraz. W tym przykładzie usuwa hello obrazu o nazwie *myOldImage* z hello *myResourceGroup*.

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a>Następne kroki

W tym samouczku utworzony niestandardowy obraz maszyny Wirtualnej. W tym samouczku omówiono:

> [!div class="checklist"]
> * Narzędzie Sysprep i generalize maszyny wirtualne
> * Tworzenie obrazu niestandardowego
> * Utwórz maszynę Wirtualną z obrazu niestandardowego
> * Wyświetlanie listy wszystkich obrazów hello w ramach subskrypcji
> * Usuń obraz

Przejdź dalej toolearn samouczka toohello o jak wysokiej dostępności maszyny wirtualnej.

> [!div class="nextstepaction"]
> [Tworzenie maszyn wirtualnych o wysokiej dostępności](tutorial-availability-sets.md)



