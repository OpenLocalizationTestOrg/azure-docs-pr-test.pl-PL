---
title: "Szybki Start - aaaAzure utworzyć Windows PowerShell maszyny Wirtualnej | Dokumentacja firmy Microsoft"
description: "Dowiesz toocreate maszyn wirtualnych systemu Windows, przy użyciu programu PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5e92435bf7ee443a01c158fed91c356363e2f425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell"></a>Tworzenie maszyny wirtualnej z systemem Windows za pomocą programu PowerShell

modułu Azure PowerShell Hello jest używany toocreate i zarządzania zasobami Azure z wiersza polecenia programu PowerShell hello lub w skryptach. Szczegóły tego przewodnika przy użyciu programu PowerShell toocreate i Azure maszyny wirtualnej z systemem Windows Server 2016. Po zakończeniu wdrażania nawiązanie połączenia toohello serwera i zainstaluj usługi IIS.  

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

To szybki start wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej. Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="log-in-tooazure"></a>Zaloguj się za tooAzure

Zaloguj się za tooyour subskrypcji platformy Azure z hello `Login-AzureRmAccount` poleceń i wykonaj hello wyświetlanymi instrukcjami.

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów platformy Azure za pomocą polecenia [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi. 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a>Tworzenie zasobów sieciowych

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a>Utwórz sieć wirtualną, podsieć i publiczny adres IP. 
Te zasoby są maszyny wirtualnej toohello łączności sieciowej tooprovide używane i podłącz go toohello internet.

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location EastUS `
    -Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location EastUS `
    -AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a>Utwórz sieciową grupę zabezpieczeń i regułę sieciowej grupy zabezpieczeń. 
grupy zabezpieczeń sieci Hello zabezpiecza hello maszyny wirtualnej za pomocą reguł ruchu przychodzącego i wychodzącego. W tym przypadku jest tworzona reguła ruchu przychodzącego dla portu 3389, która umożliwia nawiązywanie przychodzących połączeń pulpitu zdalnego. Chcemy też toocreate regułę ruchu przychodzącego dla portu 80, który zezwala na ruch przychodzący sieci web.

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP  -Protocol Tcp `
    -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
    -Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location EastUS `
    -Name myNetworkSecurityGroup -SecurityRules $nsgRuleRDP,$nsgRuleWeb
```

### <a name="create-a-network-card-for-hello-virtual-machine"></a>Utwórz karty sieciowej dla maszyny wirtualnej hello. 
Tworzenie karty sieciowej z [AzureRmNetworkInterface nowy](/powershell/module/azurerm.network/new-azurermnetworkinterface) hello maszyny wirtualnej. Karta sieciowa Hello łączy hello maszyny wirtualnej tooa podsieci, grupy zabezpieczeń sieci i publiczny adres IP.

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a>Tworzenie maszyny wirtualnej

Utwórz konfigurację maszyny wirtualnej. Ta konfiguracja zawiera ustawienia hello, które są używane podczas wdrażania maszyny wirtualnej hello, takich jak obraz, rozmiar i uwierzytelniania konfiguracji maszyny wirtualnej. Podczas wykonywania tego kroku jest wyświetlany monit o poświadczenia. wartości Hello są skonfigurowane jako hello nazwy użytkownika i hasła hello maszyny wirtualnej.

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

Utwórz maszynę wirtualną hello z [AzureRmVM nowy](/powershell/module/azurerm.compute/new-azurermvm).

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a>Podłącz maszynę toovirtual

Po zakończeniu wdrożenia hello, tworzenia połączenia pulpitu zdalnego z maszyną wirtualną hello.

Użyj hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) polecenia tooreturn hello publicznego adresu IP hello maszyny wirtualnej. Zwróć uwagę ten adres IP, więc tooit mogą łączyć się z tootest przeglądarki sieci web łączność w przyszłości kroku.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

Użyj hello następujące polecenie toocreate sesję pulpitu zdalnego z maszyną wirtualną hello. Zamień adres IP hello hello *publicznego adresu IP* maszyny wirtualnej. Po wyświetleniu monitu wprowadź poświadczenia hello używane podczas tworzenia maszyny wirtualnej hello.

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a>Instalowanie usług IIS za pośrednictwem programu PowerShell

Teraz, gdy użytkownik zalogował się toohello maszyny Wirtualnej platformy Azure, można użyć pojedynczy wiersz tooinstall PowerShell usług IIS i włączyć ruch internetowy tooallow reguły zapory lokalnej hello. Otwórz wiersz programu PowerShell i uruchom następujące polecenie hello:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a>Widok hello strona powitalna usług IIS

Zainstalowane usługi IIS i portu 80 obecnie otwarte na maszynie Wirtualnej z hello Internet można użyć przeglądarki sieci web na wybór tooview hello domyślne IIS strony powitalnej. Należy się hello toouse *publicznego adresu IP* opisane powyżej toovisit hello domyślnej strony. 

![Domyślna witryna usług IIS](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Gdy nie są już potrzebne, można użyć hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) polecenia grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a>Następne kroki

W tym przewodniku Szybki start została wdrożona prosta maszyna wirtualna i reguła sieciowej grupy zabezpieczeń oraz zainstalowano serwer sieci Web. toolearn więcej informacji o maszynach wirtualnych platformy Azure, nadal samouczek toohello dla maszyn wirtualnych systemu Windows.

> [!div class="nextstepaction"]
> [Samouczki dla maszyny wirtualnej platformy Azure z systemem Windows](./tutorial-manage-vm.md)
