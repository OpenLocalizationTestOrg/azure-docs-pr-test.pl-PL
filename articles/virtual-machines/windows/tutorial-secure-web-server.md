---
title: "Certyfikaty aaaSecure usług IIS przy użyciu protokołu SSL na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosecure hello IIS sieci web server z certyfikatów SSL na maszynie Wirtualnej systemu Windows na platformie Azure"
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
ms.date: 07/14/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 7a9e0ce07be2f55095fdb5347b64faf5caa4f7e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a>Zabezpieczenia serwera sieci web usług IIS z certyfikatów SSL na maszynie wirtualnej systemu Windows na platformie Azure
serwery sieci web toosecure, certyfikat później SSL (Secure Sockets) mogą być używane tooencrypt ruchu w sieci web. Te certyfikaty SSL mogą być przechowywane w usłudze Azure Key Vault i umożliwia bezpieczne wdrażanie certyfikatów tooWindows o maszynach wirtualnych (VM) na platformie Azure. Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tworzenie usługi Azure Key Vault
> * Generowanie lub Przekaż certyfikat toohello magazyn kluczy
> * Utwórz maszynę Wirtualną i zainstalowania serwera sieci web usług IIS hello
> * Wstaw hello certyfikatu do hello maszyny Wirtualnej i skonfiguruj program IIS wraz z powiązaniem SSL

Ten samouczek wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej. Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji. Jeśli potrzebujesz tooupgrade, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).


## <a name="overview"></a>Omówienie
Usługa Azure Key Vault zabezpiecza kluczy kryptograficznych i kluczy tajnych takich certyfikatów lub hasła. Magazyn kluczy pozwala uprościć proces zarządzania hello certyfikatu i umożliwia toomaintain kontrolę nad kluczami, które uzyskują dostęp do tych certyfikatów. Można utworzyć certyfikatu z podpisem własnym wewnątrz usługi Key Vault, lub Przekaż istniejących, zaufanego certyfikatu, który już następującą.

Zamiast przy użyciu niestandardowego obrazu maszyny Wirtualnej, który zawiera certyfikaty rozszerzania w, wstrzyknąć certyfikatów do uruchomionej maszyny Wirtualnej. Ten proces zapewnia, że certyfikaty aktualną hello są zainstalowane na serwerze sieci web podczas wdrażania. Jeśli możesz odnowić lub zastąpić certyfikat, nie masz również toocreate nowego niestandardowego obrazu maszyny Wirtualnej. Hello najnowsze certyfikaty są automatycznie dodane podczas tworzenia dodatkowych maszyn wirtualnych. W trakcie całego procesu hello certyfikaty hello nigdy nie pozostaw hello platformy Azure lub są widoczne w skrypcie, Historia wiersza polecenia lub szablonu.


## <a name="create-an-azure-key-vault"></a>Tworzenie usługi Azure Key Vault
Przed utworzeniem magazyn kluczy i certyfikatów, Utwórz nową grupę zasobów o [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupSecureWeb* w hello *wschodnie stany USA* lokalizacji:

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

Następnie należy utworzyć magazyn kluczy o [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault). Każdy magazyn kluczy wymaga unikatowej nazwy i powinna być małe litery. Zastąp `<mykeyvault>` w hello poniższy przykład z własną unikatową nazwę usługi Key Vault:

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a>Wygeneruj certyfikat i przechowywania w magazynie kluczy
W środowisku produkcyjnym, należy zaimportować prawidłowy certyfikat podpisane przez zaufanego dostawcę z [AzureKeyVaultCertificate importu](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate). W tym samouczku hello poniższym przykładzie pokazano, jak można wygenerować certyfikatu z podpisem własnym z [AzureKeyVaultCertificate Dodaj](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) czy używa hello domyślne zasady dotyczące certyfikatów z [ Nowy AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy). 

```powershell
$policy = New-AzureKeyVaultCertificatePolicy `
    -SubjectName "CN=www.contoso.com" `
    -SecretContentType "application/x-pkcs12" `
    -IssuerName Self `
    -ValidityInMonths 12

Add-AzureKeyVaultCertificate `
    -VaultName $keyvaultName `
    -Name "mycert" `
    -CertificatePolicy $policy 
```


## <a name="create-a-virtual-machine"></a>Tworzenie maszyny wirtualnej
Zestaw administratora nazwę użytkownika i hasło dla maszyny Wirtualnej z hello [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

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
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myVnet" `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleRDP"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 443
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleWWW"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name "myNic" `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS2" | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName "myVM" -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName "MicrosoftWindowsServer" `
    -Offer "WindowsServer" -Skus "2016-Datacenter" -Version "latest" | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Create virtual machine
New-AzureRmVM -ResourceGroupName $resourceGroup -Location $location -VM $vmConfig

# Use hello Custom Script Extension tooinstall IIS
Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server -IncludeManagementTools"}'
```

Trwa kilka minut, aż hello toobe maszyny Wirtualnej utworzone. Witaj ostatniego kroku jest używana hello Azure niestandardowe rozszerzenie skryptu tooinstall powitania serwera sieci web IIS z [AzureRmVmExtension zestawu](/powershell/module/azurerm.compute/set-azurermvmextension).


## <a name="add-a-certificate-toovm-from-key-vault"></a>Dodaj tooVM certyfikatu z magazynu kluczy
tooadd hello certyfikat z magazynu kluczy tooa maszyny Wirtualnej, uzyskać identyfikator hello certyfikatu z [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret). Dodaj hello certyfikatu toohello maszyny Wirtualnej z [AzureRmVMSecret Dodaj](/powershell/module/azurerm.compute/add-azurermvmsecret):

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-toouse-hello-certificate"></a>Konfigurowanie certyfikatu hello toouse usług IIS
Użyj hello niestandardowe rozszerzenie skryptu ponownie, podając [AzureRmVMExtension zestaw](/powershell/module/azurerm.compute/set-azurermvmextension) konfiguracji usług IIS hello tooupdate. Ta aktualizacja dotyczy certyfikatu hello wprowadzonym z tooIIS magazyn kluczy i konfiguruje hello powiązanie sieci web:

```powershell
$PublicSettings = '{
    "fileUris":["https://raw.githubusercontent.com/iainfoulds/azure-samples/master/secure-iis.ps1"],
    "commandToExecute":"powershell -ExecutionPolicy Unrestricted -File secure-iis.ps1"
}'

Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString $publicSettings
```


### <a name="test-hello-secure-web-app"></a>Przetestuj aplikację sieci web bezpiecznego hello
Uzyskaj hello publicznego adresu IP maszyny Wirtualnej z [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress). Witaj poniższy przykład uzyskuje hello adres IP dla `myPublicIP` utworzony wcześniej:

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

Teraz możesz otworzyć przeglądarkę sieci web i wprowadź `https://<myPublicIP>` na pasku adresu hello. Wybierz tooaccept hello ostrzeżenie o zabezpieczeniach Jeśli używasz certyfikatu z podpisem własnym, **szczegóły** , a następnie **przejdź na stronę sieci Web toohello**:

![Zaakceptuj ostrzeżenie o zabezpieczeniach przeglądarki sieci web](./media/tutorial-secure-web-server/browser-warning.png)

Jak hello poniższy przykład następnie wyświetleniem zabezpieczonej witryny sieci Web usług IIS:

![Widok działa bezpiecznej witryny usług IIS](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a>Następne kroki

W tym samouczku serwer sieci web usług IIS jest zabezpieczony za pomocą certyfikatu SSL, przechowywane w usłudze Azure Key Vault. W tym samouczku omówiono:

> [!div class="checklist"]
> * Tworzenie usługi Azure Key Vault
> * Generowanie lub Przekaż certyfikat toohello magazyn kluczy
> * Utwórz maszynę Wirtualną i zainstalowania serwera sieci web usług IIS hello
> * Wstaw hello certyfikatu do hello maszyny Wirtualnej i skonfiguruj program IIS wraz z powiązaniem SSL

Postępuj zgodnie z tym toosee łącze wstępnie skompilowany przykłady skryptów maszyny wirtualnej.

> [!div class="nextstepaction"]
> [Przykłady skryptów maszyny wirtualnej systemu Windows](./powershell-samples.md)