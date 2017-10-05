---
title: "Tworzenie maszyny Wirtualnej z do zarządzanego obrazu maszyny Wirtualnej na platformie Azure | Dokumentacja firmy Microsoft"
description: "Utwórz maszynę wirtualną systemu Windows z uogólniony obraz maszyny Wirtualnej zarządzanej przy użyciu programu Azure PowerShell w modelu wdrażania usługi Resource Manager."
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
ms.date: 05/22/2017
ms.author: cynthn
ms.openlocfilehash: 2bb2d66271178a64ec0f4642e46b23f5618a56d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-vm-from-a-managed-image"></a>Utwórz maszynę Wirtualną z zarządzanego obrazu

Możesz utworzyć wiele maszyn wirtualnych z do zarządzanego obrazu maszyny Wirtualnej na platformie Azure. Do zarządzanego obrazu maszyny Wirtualnej zawiera informacje niezbędne do tworzenia maszyn wirtualnych, dysków systemu operacyjnego i danych. Wirtualne dyski twarde, które tworzą obrazu, w tym zarówno dysków systemu operacyjnego i dysków z danymi, są przechowywane jako dyski zarządzanych. 


## <a name="prerequisites"></a>Wymagania wstępne

Musisz mieć już [utworzony obraz maszyny Wirtualnej zarządzanej](capture-image-resource.md) do użycia podczas tworzenia nowej maszyny Wirtualnej. 

Upewnij się, że najnowsze wersje modułów AzureRM.Compute i AzureRM.Network programu PowerShell. Otwórz wiersz programu PowerShell jako Administrator i uruchom następujące polecenie, aby je zainstalować.

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).



## <a name="collect-information-about-the-image"></a>Zbieranie informacji o obrazie

Najpierw musimy zebrać podstawowe informacje o obrazie i utworzyć zmienną dla obrazu. W tym przykładzie użyto do zarządzanego obrazu maszyny Wirtualnej o nazwie **myImage** w **myResourceGroup** grupy zasobów w **zachodnie centralnej nam** lokalizacji. 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a>Tworzenie sieci wirtualnej
Utwórz sieć wirtualną i podsieć [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md).

1. Utwórz podsieć. W tym przykładzie tworzy podsieć o nazwie **mySubnet** z prefiksem adresu o **10.0.0.0/24**.  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Utwórz sieć wirtualną. W tym przykładzie tworzy sieć wirtualną o nazwie **myVnet** z prefiksem adresu o **10.0.0.0/16**.  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a>Tworzenie publicznego adresu IP adres i interfejsu sieciowego

Aby umożliwić komunikację z maszyną wirtualną w sieci wirtualnej, potrzebujesz [publicznego adresu IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) i interfejsu sieciowego.

1. Utwórz publiczny adres IP. W tym przykładzie jest tworzony publiczny adres IP o nazwie **myPip**. 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Utwórz kartę sieciową. W tym przykładzie jest tworzony karty Sieciowej o nazwie **myNic**. 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-the-network-security-group-and-an-rdp-rule"></a>Tworzenie grupy zabezpieczeń sieci i reguły protokołu RDP

Aby móc zalogować się do maszyny Wirtualnej za pomocą protokołu RDP, musisz mieć reguły zabezpieczeń sieci (NSG), umożliwiająca dostęp RDP do portu 3389. 

W tym przykładzie tworzy grupy NSG o nazwie **myNsg** zawierający regułę o nazwie **myRdpRule** za pośrednictwem portu 3389 która zezwala na ruch RDP. Aby uzyskać więcej informacji na temat grup NSG, zobacz [Otwieranie portów dla maszyny Wirtualnej na platformie Azure przy użyciu programu PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-the-virtual-network"></a>Utwórz zmienną dla sieci wirtualnej

Utwórz zmienną dla ukończonych sieci wirtualnej. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-the-credentials-for-the-vm"></a>Uzyskiwanie poświadczeń dla maszyny Wirtualnej

Następujące polecenie cmdlet zostanie otwarte okno gdzie będą wprowadź nową nazwę użytkownika i hasło do użycia jako konto administratora lokalnego na zdalny dostęp do maszyny Wirtualnej. 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-the-vm-name-computer-name-and-the-size-of-the-vm"></a>Ustaw zmienne nazwę maszyny Wirtualnej, nazwy komputera i rozmiaru maszyny Wirtualnej

1. Utwórz zmienne dla nazwy komputera i nazwę maszyny Wirtualnej. W tym przykładzie nazwa maszyny Wirtualnej jako **myVM** i nazwę komputera, jako **Mój komputer**.

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. Ustaw rozmiar maszyny wirtualnej. Ten przykład tworzy **Standard_DS1_v2** rozmiaru maszyny Wirtualnej. Zobacz [rozmiarów maszyn wirtualnych](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) dokumentacji, aby uzyskać więcej informacji.

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. Dodaj nazwę maszyny Wirtualnej i rozmiar do konfiguracji maszyny Wirtualnej.

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-the-vm-image-as-source-image-for-the-new-vm"></a>Ustaw obraz maszyny Wirtualnej jako źródło obrazu dla nowej maszyny Wirtualnej

Ustaw obraz źródłowy przy użyciu Identyfikatora zarządzanego obrazu maszyny Wirtualnej.

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-the-os-configuration-and-add-the-nic"></a>Ustawienia konfiguracji systemu operacyjnego i Dodaj kartę sieciową.

Wprowadź typ magazynu (PremiumLRS lub StandardLRS) i rozmiar dysku systemu operacyjnego. W tym przykładzie typ konta w **PremiumLRS**, rozmiar dysku do **128 GB** i buforowanie dysku, aby **ReadWrite**.

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-the-vm"></a>Tworzenie maszyny wirtualnej

Tworzenie nowej maszyny wirtualnej za pomocą konfiguracji, które firma Microsoft utworzone i przechowywane w **$vm** zmiennej.

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-the-vm-was-created"></a>Sprawdź, czy maszyna wirtualna została utworzona
Po zakończeniu powinien zostać wyświetlony nowo utworzony maszyny Wirtualnej w ramach [portalu Azure](https://portal.azure.com) w obszarze **Przeglądaj** > **maszyn wirtualnych**, lub za pomocą następujących poleceń programu PowerShell:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Następne kroki
Aby zarządzać nową maszynę wirtualną w taki sposób, z programu Azure PowerShell, zobacz [tworzenia i zarządzania maszynami wirtualnymi systemu Windows za pomocą modułu Azure PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

