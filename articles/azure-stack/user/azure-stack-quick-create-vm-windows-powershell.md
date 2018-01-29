---
title: "Utwórz maszynę wirtualną z systemem Windows przy użyciu programu PowerShell w stosie Azure | Dokumentacja firmy Microsoft"
description: "Utwórz maszynę wirtualną z systemem Windows przy użyciu programu PowerShell w stosie Azure."
services: azure-stack
documentationcenter: 
author: mattbriggs
manager: femila
editor: 
ms.assetid: 7CA6C0AC-23B7-4007-BA32-7A950FD1F3B8
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 09/25/2017
ms.author: mabrigg
ms.custom: mvc
ms.openlocfilehash: 688ab6c55867d72d55e27c21c883c14ef90078d2
ms.sourcegitcommit: a5f16c1e2e0573204581c072cf7d237745ff98dc
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="create-a-windows-virtual-machine-by-using-powershell-in-azure-stack"></a>Utwórz maszynę wirtualną z systemem Windows przy użyciu programu PowerShell w stosie Azure

*Dotyczy: Azure stosu zintegrowane systemy*

Szczegóły tego przewodnika przy użyciu programu PowerShell, aby utworzyć maszynę wirtualną systemu Windows Server 2016 w stosie usługi Azure. Można wykonać kroki opisane w tym artykule z Development Kit stosu Azure lub z systemem Windows klienta zewnętrznych po nawiązaniu połączenia za pośrednictwem sieci VPN. 

## <a name="prerequisites"></a>Wymagania wstępne 

* Upewnij się, operatorem Azure stos został dodany obrazu "Windows Server 2016" do stosu Azure marketplace.  

* Stos Azure wymaga określonej wersji programu Azure PowerShell do tworzenia i zarządzania zasobami. Jeśli nie jest skonfigurowany do stosu Azure PowerShell, wykonaj kroki, aby [zainstalować](azure-stack-powershell-install.md) i [skonfigurować](azure-stack-powershell-configure-user.md) środowiska PowerShell.    

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Grupa zasobów jest kontenerem logicznym, do których stosu Azure wdrożone i zarządzane zasoby. W zestawie rozwoju lub system Azure stosu zintegrowane Uruchom następujący blok kodu, aby utworzyć grupę zasobów. Firma Microsoft zostały przypisane wartości wszystkich zmiennych w tym dokumencie, można używać ich jest lub przypisać inną wartość.  

```powershell
# Create variables to store the location and resource group names.
$location = "local"
$ResourceGroupName = "myResourceGroup"

New-AzureRmResourceGroup `
  -Name $ResourceGroupName `
  -Location $location
```

## <a name="create-storage-resources"></a>Utwórz zasoby magazynu 

Utwórz konto magazynu i kontener magazynu do przechowywania obrazu systemu Windows Server 2016.

```powershell
# Create variables to store the storage account name and the storage account SKU information
$StorageAccountName = "mystorageaccount"
$SkuName = "Standard_LRS"

# Create a new storage account
$StorageAccount = New-AzureRMStorageAccount `
  -Location $location `
  -ResourceGroupName $ResourceGroupName `
  -Type $SkuName `
  -Name $StorageAccountName

Set-AzureRmCurrentStorageAccount `
  -StorageAccountName $storageAccountName `
  -ResourceGroupName $resourceGroupName

# Create a storage container to store the virtual machine image
$containerName = 'osdisks'
$container = New-AzureStorageContainer `
  -Name $containerName `
  -Permission Blob
```

## <a name="create-networking-resources"></a>Tworzenie zasobów sieciowych

Utwórz sieć wirtualną, podsieć i publiczny adres IP. Te zasoby są używane do zapewniania łączności sieciowej do maszyny wirtualnej.  

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -Name MyVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -AllocationMethod Static `
  -IdleTimeoutInMinutes 4 `
  -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a>Tworzenie sieciowej grupy zabezpieczeń i reguły sieciowej grupy zabezpieczeń

Grupy zabezpieczeń sieci zabezpiecza maszyny wirtualnej za pomocą reguł ruchu przychodzącego i wychodzącego. Pozwala utworzyć regułę ruchu przychodzącego dla portu 3389 przychodzących połączeń usług pulpitu zdalnego i regułę ruchu przychodzącego dla portu 80, aby zezwolić na ruch przychodzący sieci web.

```powershell
# Create an inbound network security group rule for port 3389
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

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRuleWWW `
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
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRuleRDP,$nsgRuleWeb 
```
 
### <a name="create-a-network-card-for-the-virtual-machine"></a>Tworzenie karty sieciowej dla maszyny wirtualnej

Karta sieciowa łączy maszynę wirtualną z podsiecią, sieciową grupą zabezpieczeń i publicznym adresem IP.

```powershell
# Create a virtual network card and associate it with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
  -Name myNic `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id `
  -NetworkSecurityGroupId $nsg.Id 
```

## <a name="create-a-virtual-machine"></a>Tworzenie maszyny wirtualnej

Utwórz konfigurację maszyny wirtualnej. Konfiguracja obejmuje ustawienia, które są używane podczas wdrażania maszyny wirtualnej, takich jak obraz maszyny wirtualnej, rozmiar, poświadczenia.

```powershell
# Define a credential object to store the username and password for the virtual machine
$UserName='demouser'
$Password='Password@123'| ConvertTo-SecureString -Force -AsPlainText
$Credential=New-Object PSCredential($UserName,$Password)

# Create the virtual machine configuration object
$VmName = "VirtualMachinelatest"
$VmSize = "Standard_A1"
$VirtualMachine = New-AzureRmVMConfig `
  -VMName $VmName `
  -VMSize $VmSize 

$VirtualMachine = Set-AzureRmVMOperatingSystem `
  -VM $VirtualMachine `
  -Windows `
  -ComputerName "MainComputer" `
  -Credential $Credential 

$VirtualMachine = Set-AzureRmVMSourceImage `
  -VM $VirtualMachine `
  -PublisherName "MicrosoftWindowsServer" `
  -Offer "WindowsServer" `
  -Skus "2016-Datacenter" `
  -Version "latest"

$osDiskName = "OsDisk"
$osDiskUri = '{0}vhds/{1}-{2}.vhd' -f `
  $StorageAccount.PrimaryEndpoints.Blob.ToString(),`
  $vmName.ToLower(), `
  $osDiskName

# Sets the operating system disk properties on a virtual machine. 
$VirtualMachine = Set-AzureRmVMOSDisk `
  -VM $VirtualMachine `
  -Name $osDiskName `
  -VhdUri $OsDiskUri `
  -CreateOption FromImage | `
  Add-AzureRmVMNetworkInterface -Id $nic.Id 

#Create the virtual machine.
New-AzureRmVM `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -VM $VirtualMachine
```

## <a name="connect-to-the-virtual-machine"></a>Nawiązywanie połączenia z maszyną wirtualną

Aby zdalnego do maszyny wirtualnej, który został utworzony w poprzednim kroku musisz mieć publicznego adresu IP. Uruchom następujące polecenie, aby pobrać publicznego adresu IP maszyny wirtualnej: 

```powershell
Get-AzureRmPublicIpAddress `
  -ResourceGroupName $ResourceGroupName | Select IpAddress
```
 
Użyj następującego polecenia, aby utworzyć sesję pulpitu zdalnego z maszyną wirtualną. Adres IP należy zastąpić publicznego adresu IP maszyny wirtualnej. Po wyświetleniu monitu wprowadź nazwę użytkownika i hasło użyte podczas tworzenia maszyny wirtualnej.

```powershell
mstsc /v <publicIpAddress>
```

## <a name="install-iis-via-powershell"></a>Instalowanie usług IIS za pośrednictwem programu PowerShell

Teraz po zalogowaniu do maszyny wirtualnej platformy Azure możesz użyć jednego wiersza w programie PowerShell, aby zainstalować usługi IIS i włączyć lokalną regułę zapory, która zezwala na ruch w sieci Web. Otwórz wiersz polecenia programu PowerShell i uruchom następujące polecenie:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-the-iis-welcome-page"></a>Wyświetlanie strony powitalnej usług IIS

Po zainstalowaniu usług IIS i otwarciu portu 80 na maszynie wirtualnej z Internetu możesz użyć wybranej przeglądarki sieci Web, aby wyświetlić domyślną stronę powitalną przeglądarki usług IIS. Upewnij się, że w celu odwiedzenia strony domyślnej używasz udokumentowanego powyżej *publicznego adresu IP*. 

![Domyślna witryna usług IIS](./media/azure-stack-quick-create-vm-windows-powershell/default-iis-website.png) 


## <a name="delete-the-virtual-machine"></a>Usuń maszynę wirtualną

Gdy nie są już potrzebne, użyj następującego polecenia, aby usunąć grupę zasobów, która zawiera maszynę wirtualną i powiązane zasoby:

```powershell
Remove-AzureRmResourceGroup `
  -Name $ResourceGroupName
```

## <a name="next-steps"></a>Następne kroki

W tym szybkiego startu wdrożeniu prostą maszynę wirtualną systemu Windows. Aby dowiedzieć się więcej o maszynach wirtualnych Azure stosu, nadal [zagadnienia dotyczące maszyn wirtualnych w stosie Azure](azure-stack-vm-considerations.md).

