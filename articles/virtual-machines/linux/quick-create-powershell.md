---
title: "Szybki Start - aaaAzure utworzyć VM środowiska PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiesz toocreate maszyn wirtualnych systemu Linux przy użyciu programu PowerShell"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: f05ea7fedafe4fda660dc6084ae57ebf9dced473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-powershell"></a>Tworzenie maszyny wirtualnej z systemem Linux za pomocą programu PowerShell

modułu Azure PowerShell Hello jest używany toocreate i zarządzania zasobami Azure z wiersza polecenia programu PowerShell hello lub w skryptach. Szczegóły ten przewodnik przy użyciu toodeploy modułu Azure PowerShell hello maszyny wirtualnej z systemem Ubuntu server. Po wdrożeniu serwera hello połączenia SSH jest tworzony, i NGINX, serwer sieci Web jest zainstalowana.

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

To szybki start wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej. Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).

Na koniec publiczny klucz SSH o nazwie hello *id_rsa.pub* musi toobe przechowywane w hello *.ssh* katalogu profilu użytkownika systemu Windows. Aby uzyskać szczegółowe informacje na temat tworzenia kluczy SSH dla platformy Azure, zobacz [Tworzenie kluczy SSH dla platformy Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="log-in-tooazure"></a>Zaloguj się za tooAzure

Zaloguj się za tooyour subskrypcji platformy Azure z hello `Login-AzureRmAccount` poleceń i wykonaj hello wyświetlanymi instrukcjami.

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów platformy Azure za pomocą polecenia [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi. 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
```

## <a name="create-networking-resources"></a>Tworzenie zasobów sieciowych

Utwórz sieć wirtualną, podsieć i publiczny adres IP. Te zasoby są maszyny wirtualnej toohello łączności sieciowej tooprovide używane i podłącz go toohello internet.

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location eastus `
-Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location eastus `
-AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

Utwórz sieciową grupę zabezpieczeń i regułę sieciowej grupy zabezpieczeń. grupy zabezpieczeń sieci Hello zabezpiecza hello maszyny wirtualnej za pomocą reguł ruchu przychodzącego i wychodzącego. W tym przypadku jest tworzona reguła ruchu przychodzącego dla portu 22, która umożliwia nawiązywanie przychodzących połączeń SSH. Chcemy też toocreate regułę ruchu przychodzącego dla portu 80, który zezwala na ruch przychodzący sieci web.

```powershell
# Create an inbound network security group rule for port 22
$nsgRuleSSH = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleSSH  -Protocol Tcp `
-Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 22 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
-Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location eastus `
-Name myNetworkSecurityGroup -SecurityRules $nsgRuleSSH,$nsgRuleWeb
```

Tworzenie karty sieciowej z [AzureRmNetworkInterface nowy](/powershell/module/azurerm.network/new-azurermnetworkinterface) hello maszyny wirtualnej. Karta sieciowa Hello łączy hello maszyny wirtualnej tooa podsieci, grupy zabezpieczeń sieci i publiczny adres IP.

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a>Tworzenie maszyny wirtualnej

Utwórz konfigurację maszyny wirtualnej. Ta konfiguracja zawiera ustawienia hello, które są używane podczas wdrażania maszyny wirtualnej hello, takich jak obraz, rozmiar i uwierzytelniania konfiguracji maszyny wirtualnej.

```powershell
# Define a credential object
$securePassword = ConvertTo-SecureString ' ' -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ("azureuser", $securePassword)

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Linux -ComputerName myVM -Credential $cred -DisablePasswordAuthentication | `
Set-AzureRmVMSourceImage -PublisherName Canonical -Offer UbuntuServer -Skus 14.04.2-LTS -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Configure SSH Keys
$sshPublicKey = Get-Content "$env:USERPROFILE\.ssh\id_rsa.pub"
Add-AzureRmVMSshPublicKey -VM $vmconfig -KeyData $sshPublicKey -Path "/home/azureuser/.ssh/authorized_keys"
```

Utwórz maszynę wirtualną hello z [AzureRmVM nowy](/powershell/module/azurerm.compute/new-azurermvm).

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a>Podłącz maszynę toovirtual

Po zakończeniu wdrożenia hello, należy utworzyć połączenie SSH z maszyną wirtualną hello.

Użyj hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) polecenia tooreturn hello publicznego adresu IP hello maszyny wirtualnej.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

Z systemu przy użyciu protokołu SSH zainstalowany hello używane następujące polecenie maszyny wirtualnej toohello tooconnect. Jeśli działa w systemie Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) mogą być używane toocreate hello połączenia. 

```bash 
ssh <Public IP Address>
```

Po wyświetleniu monitu, nazwa użytkownika logowania hello jest *azureuser*. Wprowadzone hasło podczas tworzenia kluczy SSH, należy najpierw tooenter w tym również.


## <a name="install-nginx"></a>Instalowanie serwera NGINX

Użyj następujących hello bash źródła pakietów tooupdate skryptu i zainstaluj najnowszy pakiet NGINX hello. 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-ngix-welcome-page"></a>Wyświetlanie hello NGIX strony powitalnej

NGINX zainstalowane i numer portu 80 obecnie otwarte na maszynie Wirtualnej z hello Internet — można użyć przeglądarki sieci web na wybór tooview hello domyślne NGINX strony powitalnej. Należy się toouse hello publicznego adresu IP, który opisane powyżej toovisit hello domyślnej strony. 

![Domyślna witryna serwera NGINX](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Gdy nie są już potrzebne, można użyć hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) polecenia grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a>Następne kroki

W tym przewodniku Szybki start została wdrożona prosta maszyna wirtualna i reguła sieciowej grupy zabezpieczeń oraz zainstalowano serwer sieci Web. toolearn więcej informacji o maszynach wirtualnych platformy Azure, nadal samouczek toohello dla maszyn wirtualnych systemu Linux.

> [!div class="nextstepaction"]
> [Samouczki dla maszyny wirtualnej platformy Azure z systemem Linux](./tutorial-manage-vm.md)
