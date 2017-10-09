---
title: aaaCustomize maszyny Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse hello niestandardowe rozszerzenie skryptu i toocustomize Key Vault maszyn wirtualnych systemu Windows na platformie Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c03b2bb6d70875134c63ea2fe4c2e2c1777c2188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-windows-virtual-machine-in-azure"></a>Jak toocustomize maszynę wirtualną systemu Windows na platformie Azure
wymagane jest zwykle tooconfigure maszynach wirtualnych (VM) w sposób szybki i spójne jakiegoś automatyzacji. Typowe toocustomize podejście Maszynę wirtualną systemu Windows jest toouse [niestandardowe rozszerzenie skryptu systemu Windows](extensions-customscript.md). Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Użyj hello niestandardowe rozszerzenie skryptu tooinstall usług IIS
> * Utwórz maszynę Wirtualną, która używa hello niestandardowe rozszerzenie skryptu
> * Wyświetl uruchomionej witryny usług IIS, po zastosowaniu hello rozszerzenia

Ten samouczek wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej. Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji. Jeśli potrzebujesz tooupgrade, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).


## <a name="custom-script-extension-overview"></a>Omówienie rozszerzenia niestandardowego skryptu
Witaj niestandardowe rozszerzenie skryptu pobiera i uruchamia skrypty na maszynach wirtualnych Azure. To rozszerzenie jest przydatne w przypadku konfiguracji wdrożenia post, instalacja oprogramowania lub dowolnej innej konfiguracji / zadanie zarządzania. Skryptów można pobrać z magazynu Azure lub usługi GitHub lub podane toohello portalu Azure w rozszerzeniu czas wykonywania.

Hello rozszerzenia niestandardowego skryptu integruje się z szablonów usługi Azure Resource Manager i można również uruchomić przy użyciu hello wiersza polecenia platformy Azure, programu PowerShell, portalu Azure lub hello interfejsu API REST maszyny wirtualnej Azure.

W systemach Windows i maszyn wirtualnych systemu Linux, można użyć hello niestandardowe rozszerzenie skryptu.


## <a name="create-virtual-machine"></a>Tworzenie maszyny wirtualnej
Przed utworzeniem maszyny Wirtualnej, Utwórz nową grupę zasobów o [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupAutomate* w hello *EastUS* lokalizacji:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupAutomate -Location EastUS
```

Ustaw nazwę użytkownika i hasło administratora dla maszyn wirtualnych hello z [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Teraz możesz utworzyć maszynę Wirtualną za pomocą hello [AzureRmVM nowy](/powershell/module/azurerm.compute/new-azurermvm). Witaj poniższy przykład tworzy hello wymagane składniki sieci wirtualnej, konfiguracja hello systemu operacyjnego, a następnie tworzy Maszynę wirtualną o nazwie *myVM*:

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleWWW  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName myResourceGroupAutomate -Location EastUS -VM $vmConfig
```

Trwa kilka minut, aż hello zasobów i utworzyć toobe maszyny Wirtualnej.


## <a name="automate-iis-install"></a>Automatyzowanie instalacji usług IIS
Użyj [AzureRmVMExtension zestaw](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello niestandardowe rozszerzenie skryptu. Witaj uruchamia rozszerzenia `powershell Add-WindowsFeature Web-Server` tooinstall hello serwer sieci Web usług IIS, a następnie aktualizacje hello *Default.htm* strony tooshow hello nazwy hosta hello maszyny Wirtualnej:

```powershell
Set-AzureRmVMExtension -ResourceGroupName myResourceGroupAutomate `
    -ExtensionName IIS `
    -VMName myVM `
    -Publisher Microsoft.Compute `
    -ExtensionType CustomScriptExtension `
    -TypeHandlerVersion 1.4 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
    -Location EastUS
```


## <a name="test-web-site"></a>Test witryny sieci web
Uzyskaj hello publicznego adresu IP z usługi równoważenia obciążenia z [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Witaj poniższy przykład uzyskuje hello adres IP dla *myPublicIP* utworzony wcześniej:

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Name myPublicIP | select IpAddress
```

W przeglądarce sieci web tooa można następnie wprowadzić hello publicznego adresu IP. Hello witryny sieci Web jest wyświetlany, łącznie z nazwą hosta hello hello maszyny Wirtualnej tego modułu równoważenia obciążenia hello rozproszonych tooas ruchu w hello poniższy przykład:

![Witryna sieci Web IIS uruchomiona](./media/tutorial-automate-vm-deployment/running-iis-website.png)


## <a name="next-steps"></a>Następne kroki

W tym samouczku automatycznego jest hello instalacji usług IIS na maszynie Wirtualnej. W tym samouczku omówiono:

> [!div class="checklist"]
> * Użyj hello niestandardowe rozszerzenie skryptu tooinstall usług IIS
> * Utwórz maszynę Wirtualną, która używa hello niestandardowe rozszerzenie skryptu
> * Wyświetl uruchomionej witryny usług IIS, po zastosowaniu hello rozszerzenia

Jak przejść dalej toolearn samouczka toohello toocreate niestandardowych obrazów maszyn wirtualnych.

> [!div class="nextstepaction"]
> [Tworzenie niestandardowych obrazów maszyn wirtualnych](./tutorial-custom-images.md)
