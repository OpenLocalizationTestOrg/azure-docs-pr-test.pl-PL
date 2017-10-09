---
title: "aaaCreate maszyny Wirtualnej z do zarządzanego obrazu maszyny Wirtualnej na platformie Azure | Dokumentacja firmy Microsoft"
description: "Utwórz maszynę wirtualną systemu Windows z uogólniony obraz maszyny Wirtualnej zarządzanego w modelu wdrażania usługi Resource Manager hello przy użyciu programu Azure PowerShell."
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
ms.openlocfilehash: 5036ef1533c144a9a328e94599b359e0166f337d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-managed-image"></a>Utwórz maszynę Wirtualną z zarządzanego obrazu

Możesz utworzyć wiele maszyn wirtualnych z do zarządzanego obrazu maszyny Wirtualnej na platformie Azure. Do zarządzanego obrazu maszyny Wirtualnej zawiera hello informacje niezbędne toocreate maszyny Wirtualnej, włączając hello systemu operacyjnego i dysków z danymi. Witaj, które tworzą obrazu hello, w tym zarówno dyski hello systemu operacyjnego i dysków z danymi, są przechowywane jako zarządzane dyski wirtualne dyski twarde. 


## <a name="prerequisites"></a>Wymagania wstępne

Należy toohave już [utworzony obraz maszyny Wirtualnej zarządzanej](capture-image-resource.md) toouse tworzenia hello nowej maszyny Wirtualnej. 

Upewnij się, że najnowsze wersje hello hello modułów AzureRM.Compute i AzureRM.Network programu PowerShell. Otwórz wiersz programu PowerShell jako Administrator i uruchom następujące polecenie tooinstall hello je.

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).



## <a name="collect-information-about-hello-image"></a>Zbieranie informacji o hello obrazu

Najpierw możemy toogather podstawowe informacje o obrazie hello i Tworzenie zmiennej hello obrazu. W tym przykładzie użyto do zarządzanego obrazu maszyny Wirtualnej o nazwie **myImage** będący w hello **myResourceGroup** grupy zasobów w hello **zachodnie centralnej nam** lokalizacji. 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a>Tworzenie sieci wirtualnej
Tworzenie sieci wirtualnej hello i podsieci hello [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md).

1. Utwórz podsieć hello. W tym przykładzie tworzy podsieć o nazwie **mySubnet** z prefiksu adresu hello **10.0.0.0/24**.  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Utwórz sieć wirtualną hello. W tym przykładzie tworzy sieć wirtualną o nazwie **myVnet** z prefiksu adresu hello **10.0.0.0/16**.  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a>Tworzenie publicznego adresu IP adres i interfejsu sieciowego

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

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Tworzenie grupy zabezpieczeń sieci hello i reguły protokołu RDP

toobe stanie toolog w tooyour maszyny Wirtualnej przy użyciu protokołu RDP, należy toohave reguły zabezpieczeń sieci (NSG), umożliwiająca dostęp RDP do portu 3389. 

W tym przykładzie tworzy grupy NSG o nazwie **myNsg** zawierający regułę o nazwie **myRdpRule** za pośrednictwem portu 3389 która zezwala na ruch RDP. Aby uzyskać więcej informacji na temat grup NSG, zobacz [otwierania portów tooa maszyny Wirtualnej na platformie Azure przy użyciu programu PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

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


## <a name="create-a-variable-for-hello-virtual-network"></a>Utwórz zmienną hello sieci wirtualnej

Utwórz zmienną ukończyć powitalnych sieci wirtualnej. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a>Uzyskać poświadczenia hello hello maszyny Wirtualnej

Witaj następującego polecenia cmdlet zostanie otwarte okno którym wprowadza użytkownika nowe toouse nazwę i hasło jako hello konta administratora lokalnego na zdalny dostęp do hello maszyny Wirtualnej. 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-hello-vm-name-computer-name-and-hello-size-of-hello-vm"></a>Ustaw zmienne hello maszyny Wirtualnej name, nazwa komputera i hello rozmiar hello maszyny Wirtualnej

1. Utwórz zmienne hello maszyny Wirtualnej i nazwy komputera. W tym przykładzie nazwa maszyny Wirtualnej hello jako **myVM** i nazwa komputera hello jako **Mój komputer**.

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. Ustaw rozmiar hello hello maszyny wirtualnej. Ten przykład tworzy **Standard_DS1_v2** rozmiaru maszyny Wirtualnej. Zobacz hello [rozmiarów maszyn wirtualnych](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) dokumentacji, aby uzyskać więcej informacji.

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. Dodaj hello nazwę maszyny Wirtualnej i konfiguracji maszyny Wirtualnej toohello rozmiar.

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a>Obraz maszyny Wirtualnej hello zestawu jako obraz źródłowy dla hello nowej maszyny Wirtualnej

Ustaw obraz źródłowy hello przy użyciu Identyfikatora hello hello zarządzanego obrazu maszyny Wirtualnej.

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a>Ustawienia konfiguracji systemu operacyjnego hello i Dodaj hello karty sieciowej.

Wprowadź typ magazynu hello (PremiumLRS lub StandardLRS) i hello rozmiar dysku systemu operacyjnego hello. W tym przykładzie typ konta hello zbyt**PremiumLRS**, zbyt hello rozmiar dysku**128 GB** i buforowania dysku zbyt**ReadWrite**.

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a>Utwórz hello maszyny Wirtualnej

Tworzenie nowej maszyny wirtualnej za pomocą hello konfiguracji, które firma Microsoft utworzone i przechowywane w hello hello **$vm** zmiennej.

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a>Sprawdź hello, że maszyna wirtualna została utworzona
Po zakończeniu powinien zostać wyświetlony hello nowo utworzony maszyny Wirtualnej w hello [portalu Azure](https://portal.azure.com) w obszarze **Przeglądaj** > **maszyn wirtualnych**, lub za pomocą następujących hello Polecenia programu PowerShell:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Następne kroki
toomanage nowej maszyny wirtualnej przy użyciu programu Azure PowerShell, zobacz [tworzenia i zarządzania maszynami wirtualnymi systemu Windows za pomocą modułu Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

