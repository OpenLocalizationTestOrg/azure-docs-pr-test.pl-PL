---
title: "aaaCreate i zarządzania maszynami wirtualnymi systemu Windows na platformie Azure używanego przez wiele kart sieciowych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate i zarządzanie nimi maszyny Wirtualnej systemu Windows, który ma wiele kart sieciowych tooit dołączone przy użyciu szablonów programu Azure PowerShell lub Menedżera zasobów."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 9bff5b6d-79ac-476b-a68f-6f8754768413
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: c3c7d7569aca6f047238146d84b2ffccf05d4079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a>Tworzenie i zarządzanie nimi maszyny wirtualnej systemu Windows, który ma wiele kart sieciowych
Maszynach wirtualnych (VM) na platformie Azure mogą mieć wiele toothem kart sieciowych dołączonych interfejsu sieci wirtualnej. Typowy scenariusz obejmuje toohave w różnych podsieciach łączności frontonu i zaplecza, lub sieci dedykowanej tooa monitorowania lub tworzenia kopii zapasowych. W tym artykule szczegółowo sposób toocreate maszynę Wirtualną, która ma wiele kart sieciowych dołączonych tooit. Możesz także dowiedzieć się, jak tooadd lub usuń karty sieciowe z istniejącej maszyny Wirtualnej. Różne [rozmiarów maszyn wirtualnych](sizes.md) obsługuje różną liczbę kart sieciowych, więc odpowiednio rozmiar maszyny Wirtualnej.

Aby uzyskać szczegółowe informacje, łącznie ze sposobem toocreate wiele kart sieciowych w ramach własnych skryptów środowiska PowerShell, zobacz [wdrażanie maszyn wirtualnych kart Sieciowych na wielu](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).

## <a name="prerequisites"></a>Wymagania wstępne
Upewnij się, że masz hello [najnowszą wersję programu Azure PowerShell zainstalowany i skonfigurowany](/powershell/azure/overview).

Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametru zawierają *myResourceGroup*, *myVnet*, i *myVM*.


## <a name="create-a-vm-with-multiple-nics"></a>Tworzenie maszyny wirtualnej z wieloma kartami sieciowymi
Najpierw utwórz grupę zasobów. Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *EastUs* lokalizacji:

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a>Tworzenie sieci wirtualnej i podsieci
Typowy scenariusz dotyczy toohave sieci wirtualnej co najmniej dwie podsieci. W jednej podsieci może być w przypadku ruchu frontonu hello innych transmisji zaplecza. tooconnect tooboth podsieci, można następnie używać wielu kart sieciowych na maszynie Wirtualnej.

1. Zdefiniuj dwie podsieci sieci wirtualnej z [AzureRmVirtualNetworkSubnetConfig nowy](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig). Witaj poniższym przykładzie zdefiniowano hello podsieci dla *mySubnetFrontEnd* i *mySubnetBackEnd*:

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. Tworzenie sieci wirtualnej i podsieci z [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). Witaj poniższy przykład tworzy sieć wirtualną o nazwie *myVnet*:

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a>Tworzenie wielu kart sieciowych
Utwórz dwie karty sieciowe z [AzureRmNetworkInterface nowy](/powershell/module/azurerm.network/new-azurermnetworkinterface). Dołącz jednej podsieci frontonu toohello karty Sieciowej i jedną podsieć zaplecza toohello karty Sieciowej. Witaj poniższy przykład tworzy karty sieciowe o nazwie *myNic1* i *myNic2*:

```powershell
$frontEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetFrontEnd'}
$myNic1 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic1" `
    -Location "EastUs" `
    -SubnetId $frontEnd.Id

$backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}
$myNic2 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic2" `
    -Location "EastUs" `
    -SubnetId $backEnd.Id
```

Zwykle również utworzyć [sieciowej grupy zabezpieczeń](../../virtual-network/virtual-networks-nsg.md) lub [modułu równoważenia obciążenia](../../load-balancer/load-balancer-overview.md) toohelp zarządzania i rozpowszechniają ruch maszyn wirtualnych. Witaj [bardziej szczegółowe wielu kart Sieciowych maszyny Wirtualnej](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) artykule opisano tworzenie grupy zabezpieczeń sieci i przypisywanie kart sieciowych.

### <a name="create-hello-virtual-machine"></a>Utwórz maszynę wirtualną hello
Teraz uruchomić toobuild konfiguracji maszyny Wirtualnej. Rozmiar każdej maszyny Wirtualnej ma limit hello całkowitą liczbę kart sieciowych, że można dodawać tooa maszyny Wirtualnej. Aby uzyskać więcej informacji, zobacz [rozmiarów maszyn wirtualnych systemu Windows](sizes.md).

1. Ustaw toohello poświadczenia sieci VM `$cred` zmiennej w następujący sposób:

    ```powershell
    $cred = Get-Credential
    ```

2. Zdefiniuj maszyny Wirtualnej z [nowe AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig). Witaj poniższym przykładzie zdefiniowano maszyny Wirtualnej o nazwie *myVM* i używa rozmiar maszyny Wirtualnej, która obsługuje więcej niż dwie karty sieciowe (*Standard_DS3_v2*):

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. Utwórz hello reszty konfiguracji maszyny Wirtualnej z [AzureRmVMOperatingSystem zestaw](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) i [AzureRmVMSourceImage zestawu](/powershell/module/azurerm.compute/set-azurermvmsourceimage). Witaj poniższy przykład tworzy Maszynę wirtualną systemu Windows Server 2016:

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig `
        -Windows `
        -ComputerName "myVM" `
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig `
        -PublisherName "MicrosoftWindowsServer" `
        -Offer "WindowsServer" `
        -Skus "2016-Datacenter" `
        -Version "latest"
   ```

4. Dołącz Witaj dwie karty sieciowe, wcześniej utworzone przy użyciu [AzureRmVMNetworkInterface Dodaj](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. Na koniec należy utworzyć maszyny Wirtualnej z [AzureRmVM nowy](/powershell/module/azurerm.compute/new-azurermvm):

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-tooan-existing-vm"></a>Dodaj tooan karty Sieciowej, istniejącej maszyny Wirtualnej
Dodaj tooadd wirtualnego tooan kart istniejącej maszyny Wirtualnej, deallocate hello maszyny Wirtualnej, hello wirtualnej karty Sieciowej, a następnie uruchomić hello maszyny Wirtualnej.

1. Cofnięcie przydziału hello maszyny Wirtualnej z [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm). Witaj poniższy przykład cofa alokację hello maszyny Wirtualnej o nazwie *myVM* w *myResourceGroup*:

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. Pobierz hello istniejącej konfiguracji hello maszyny Wirtualnej z [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm). Witaj poniższy przykład pobiera informacje o hello maszyny Wirtualnej o nazwie *myVM* w *myResourceGroup*:

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. Witaj poniższy przykład tworzy wirtualnej karty Sieciowej z [AzureRmNetworkInterface nowy](/powershell/module/azurerm.network/new-azurermnetworkinterface) o nazwie *myNic3* dołączona za*mySubnetBackEnd*. Witaj wirtualnej karty Sieciowej jest dołączony toohello maszyny Wirtualnej o nazwie *myVM* w *myResourceGroup* z [AzureRmVMNetworkInterface Dodaj](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

    ```powershell
    # Get info for hello back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get hello ID of hello new virtual NIC and add tooVM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a>Podstawowy wirtualnych kart sieciowych
    Jedną z kart sieciowych w maszynie Wirtualnej z wieloma kartami Sieciowymi hello musi toobe podstawowej. Jeśli jeden z hello istniejących wirtualnych kart sieciowych na powitania maszyna wirtualna jest już ustawiony jako podstawowy, możesz pominąć ten krok. Witaj poniższym przykładzie założono, że dwie wirtualne karty sieciowe teraz znajdują się na maszynie Wirtualnej i chcesz tooadd hello pierwszej karty Sieciowej (`[0]`) jako podstawowy hello:
        
    ```powershell
    # List existing NICs on hello VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 toobe primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update hello VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. Uruchom hello maszyny Wirtualnej z [Start AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a>Usuń z istniejącej maszyny Wirtualnej karty Sieciowej
tooremove wirtualnej karty Sieciowej z istniejącej maszyny Wirtualnej, deallocate hello maszyna wirtualna, Usuń hello wirtualnej karty Sieciowej, a następnie hello uruchomienia maszyny Wirtualnej.

1. Cofnięcie przydziału hello maszyny Wirtualnej z [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm). Witaj poniższy przykład cofa alokację hello maszyny Wirtualnej o nazwie *myVM* w *myResourceGroup*:

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. Pobierz hello istniejącej konfiguracji hello maszyny Wirtualnej z [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm). Witaj poniższy przykład pobiera informacje o hello maszyny Wirtualnej o nazwie *myVM* w *myResourceGroup*:

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. Pobierz informacje o hello Usuń kartę Sieciową z [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface). Witaj poniższy przykład pobiera informacje *myNic3*:

    ```powershell
    # List existing NICs on hello VM if you need toodetermine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. Usuń hello kartą Sieciową o [AzureRmVMNetworkInterface Usuń](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) , a następnie aktualizacji hello maszyny Wirtualnej z [AzureRmVm aktualizacji](/powershell/module/azurerm.compute/update-azurermvm). Witaj poniższy przykład umożliwia usunięcie *myNic3* uzyskanych przez `$nicId` w hello poprzedzających krok:

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. Uruchom hello maszyny Wirtualnej z [Start AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a>Tworzenie wielu kart sieciowych z szablonami
Szablony usługi Azure Resource Manager Podaj toocreate sposób wielu wystąpień zasobu podczas wdrażania, takich jak tworzenie wielu kart sieciowych. Szablony Menedżera zasobów za pomocą deklaratywne toodefine pliki JSON Twojego środowiska. Aby uzyskać więcej informacji, zobacz [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). Można użyć *kopiowania* toospecify hello liczbę wystąpień toocreate:

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

Aby uzyskać więcej informacji, zobacz [tworzenie wielu wystąpień przy użyciu *kopiowania*](../../resource-group-create-multiple.md). 

Można również użyć `copyIndex()` tooappend numer tooa Nazwa zasobu. Następnie możesz utworzyć *myNic1*, *MyNic2* i tak dalej. Witaj poniższy kod przedstawia przykład dołączanie wartość indeksu hello:

```json
"name": "[concat('myNic', copyIndex())]", 
```

Pełny przykład można znaleźć [tworzenia wielu kart sieciowych przy użyciu szablonów usługi Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).

## <a name="next-steps"></a>Następne kroki
Przegląd [rozmiarów maszyn wirtualnych systemu Windows](sizes.md) Jeśli próbujesz toocreate maszynę Wirtualną, która ma wiele kart sieciowych. Należy zwrócić uwagę toohello maksymalną liczbę kart sieciowych obsługiwanych przez każdy rozmiar maszyny Wirtualnej. 


