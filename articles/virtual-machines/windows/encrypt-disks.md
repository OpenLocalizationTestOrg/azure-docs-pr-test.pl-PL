---
title: aaaEncrypt dyski na maszynie Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Jak tooencrypt dyski wirtualne na maszynie Wirtualnej systemu Windows dla zwiększonych zabezpieczeń przy użyciu programu Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/10/2017
ms.author: iainfou
ms.openlocfilehash: 77c42a67cb57a9dc5fe3159fce0be75e3a965be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-windows-vm"></a>Jak tooencrypt dyski wirtualne na maszynie Wirtualnej systemu Windows
Ulepszone maszyny wirtualnej (VM) zabezpieczeń i zgodności mogą być szyfrowane dyski wirtualne na platformie Azure. Dyski są szyfrowane za pomocą kluczy kryptograficznych, które są już zabezpieczone w usłudze Azure Key Vault. Kontrolowanie tych kluczy kryptograficznych i przeprowadzić inspekcję ich używania. Ten sposób artykuł szczegóły tooencrypt dyski wirtualne na maszynie Wirtualnej z systemem Windows przy użyciu programu Azure PowerShell. Możesz również [szyfrowania maszyny Wirtualnej systemu Linux przy użyciu hello Azure CLI 2.0](../linux/encrypt-disks.md).

## <a name="overview-of-disk-encryption"></a>Omówienie szyfrowania dysków
Dyski wirtualne na maszynach wirtualnych systemu Windows są szyfrowane, gdy za pomocą funkcji Bitlocker. Jest bezpłatna dla szyfrowania dysków wirtualnych na platformie Azure. Klucze szyfrowania są przechowywane w usługi Azure Key Vault przy użyciu ochrony oprogramowania, lub możesz zaimportować lub wygenerować klucze w sprzętowych modułach zabezpieczeń (HSM) certyfikowane tooFIPS 140-2 poziom 2 standardów. Te klucze szyfrowania są używane tooencrypt i odszyfrowywania tooyour dołączonych dysków wirtualnych maszyny Wirtualnej. Zachowanie kontroli nad tych kluczy kryptograficznych i przeprowadzić inspekcję ich używania. Nazwy głównej usługi Azure Active Directory zapewnia mechanizm bezpiecznego do wystawiania tych kluczy kryptograficznych, ponieważ maszyny wirtualne są zasilane i wyłączanie.

proces Hello szyfrowania maszyny Wirtualnej przebiega w następujący sposób:

1. Tworzenie klucza kryptograficznego w usłudze Azure Key Vault.
2. Skonfiguruj hello kryptograficznych klucza toobe można używać do szyfrowania dysków.
3. klucz kryptograficzny hello tooread z hello Azure Key Vault, Utwórz usługę Azure Active Directory podmiotu zabezpieczeń z odpowiednimi uprawnieniami hello.
4. Wystawiać tooencrypt polecenia hello wirtualnych dysków, określenie nazwy głównej usługi Azure Active Directory hello i odpowiednie toobe klucza kryptograficznego używane.
5. główne żądania usługi Azure Active Directory Hello hello wymaganego klucza kryptograficznego z usługi Azure Key Vault.
6. dyski wirtualne Hello są szyfrowane za pomocą klucza kryptograficznego hello podane.

## <a name="encryption-process"></a>Proces szyfrowania
Szyfrowanie dysków opiera się na powitania następujące dodatkowe składniki:

* **Usługa Azure Key Vault** — używane toosafeguard kluczy kryptograficznych i kluczy tajnych używane podczas procesu szyfrowania i odszyfrowywania dysku hello. 
  * Jeśli istnieje, można użyć istniejącego magazynu kluczy Azure. Nie masz toodedicate dysków tooencrypting magazynu kluczy.
  * granice administracyjne tooseparate i widoczności klucza, można utworzyć dedykowane Key Vault.
* **Usługa Azure Active Directory** — Witaj uchwytów bezpiecznej wymiany kluczy kryptograficznych wymagane i uwierzytelniania dla żądanej akcji. 
  * Zazwyczaj można użyć istniejącego wystąpienia usługi Azure Active Directory, do przechowywania aplikacji.
  * nazwy głównej usługi Hello zapewnia toorequest mechanizmu bezpiecznego i wydawane hello odpowiednich kluczy kryptograficznych. Nie opracowujesz aplikację rzeczywista, która integruje się z usługą Azure Active Directory.

## <a name="requirements-and-limitations"></a>Wymagania i ograniczenia
Obsługiwane scenariusze i wymagania dotyczące szyfrowania dysków:

* Włączenie szyfrowania na nowych maszyn wirtualnych systemu Windows z portalu Azure Marketplace obrazy lub niestandardowego obrazu wirtualnego dysku twardego.
* Włączenie szyfrowania na istniejących maszyn wirtualnych systemu Windows na platformie Azure.
* Włączenie szyfrowania na maszynach wirtualnych systemu Windows, które są skonfigurowane przy użyciu funkcji miejsca do magazynowania.
* Wyłączenie szyfrowania systemu operacyjnego i danych dyski dla maszyn wirtualnych systemu Windows.
* Wszystkie zasoby (na przykład usługi Key Vault, konta magazynu i maszyny Wirtualnej) musi być w hello tego samego regionu Azure i subskrypcji.
* Warstwy standardowa maszyn wirtualnych, takie jak, D, DS, G i GS serii maszyn wirtualnych.

Szyfrowanie dysków nie jest obecnie obsługiwane w hello następujące scenariusze:

* Maszyny wirtualne warstwy podstawowa.
* Maszyny wirtualne utworzone za pomocą hello klasycznego modelu wdrożenia.
* Aktualizowanie kluczy kryptograficznych hello na maszynie Wirtualnej platformy już zaszyfrowany.
* Integracja z usługą zarządzania kluczami lokalnego.

## <a name="create-azure-key-vault-and-keys"></a>Tworzenie usługi Azure Key Vault i kluczy
Przed rozpoczęciem upewnij się, najnowszą wersję hello tego hello Azure PowerShell moduł został zainstalowany. Aby uzyskać więcej informacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview). W przykładach poleceń hello Zamień wszystkie parametry przykład własne nazwy, lokalizacji i wartości klucza. Witaj następujących przykładach użyto Konwencji *myResourceGroup*, *myKeyVault*, *myVM*itp.

pierwszym krokiem Hello jest toocreate toostore usługi Azure Key Vault kluczy kryptograficznych. Usługa Azure Key Vault może przechowywać klucze i klucze tajne, lub haseł, które pozwalają toosecurely wdrożyć je w aplikacji i usług. Szyfrowanie dysków wirtualnych tworzenia toostore Key Vault klucza kryptograficznego, który jest używany tooencrypt lub odszyfrować dysków wirtualnych. 

Włącz hello dostawcy usługi Azure Key Vault w ramach Twojej subskrypcji platformy Azure z [AzureRmResourceProvider rejestru](/powershell/module/azurerm.resources/register-azurermresourceprovider), następnie utwórz nową grupę zasobów o [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Witaj poniższy przykład tworzy nazwę grupy zasobów *myResourceGroup* w hello *wschodnie stany USA* lokalizacji:

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

Hello Azure Key Vault zawierającego hello kluczy kryptograficznych i obliczeniowe skojarzone zasoby, takie jak magazyn i hello samej maszyny Wirtualnej musi znajdować się w hello tego samego regionu. Tworzenie usługi Azure Key Vault z [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) i Włącz hello Key Vault służących do szyfrowania dysku. Określ unikatową nazwę usługi Key Vault *keyVaultName* w następujący sposób:

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

Mogą być przechowywane przy użyciu oprogramowania lub sprzętu modelu zabezpieczeń (HSM) ochronę kluczy kryptograficznych. Użycie modułów HSM wymaga premium magazynu kluczy. Brak dodatkowych kosztów toocreating premium magazynu kluczy, a nie standardowy magazyn kluczy, którego przechowuje klucze chronione przez oprogramowanie. toocreate premium usługi Key Vault w hello poprzedzających krok dodać hello *- Sku "Premium"* parametrów. Witaj poniższym przykładzie użyto klucze chronione oprogramowaniem ponieważ utworzyliśmy standardowy magazyn kluczy. 

W przypadku obu modeli ochrony hello platformy Azure musi toobe udzielać dostępu do kluczy kryptograficznych hello toorequest, w przypadku, gdy hello maszyny Wirtualnej wykonuje rozruch toodecrypt hello wirtualnych dysków. Tworzenie klucza kryptograficznego w magazyn kluczy o [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey). Witaj poniższym przykładzie jest tworzony klucz o nazwie *klucze*:

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-hello-azure-active-directory-service-principal"></a>Utwórz hello nazwy głównej usługi Azure Active Directory
Gdy dyski wirtualne są szyfrowane lub odszyfrować, należy określić konto toohandle hello uwierzytelniania i wymiana kluczy kryptograficznych z magazynu kluczy. To konto, nazwy głównej usługi Azure Active Directory umożliwia toorequest platformy Azure hello hello odpowiednich kluczy kryptograficznych imieniu hello maszyny Wirtualnej. Domyślne wystąpienie usługi Azure Active Directory jest dostępne w Twojej subskrypcji, chociaż w wielu organizacjach są wyposażone w dedykowane katalogów usługi Azure Active Directory.

Tworzenie nazwy głównej usługi w usłudze Azure Active Directory z [AzureRmADServicePrincipal nowy](/powershell/module/azurerm.resources/new-azurermadserviceprincipal). toospecify bezpieczne hasło, należy wykonać hello [ograniczenia w usłudze Azure Active Directory i zasadami haseł](../../active-directory/active-directory-passwords-policy.md):

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

toosuccessfully zaszyfrować lub odszyfrować dysków wirtualnych, uprawnienia do klucza kryptograficznego hello przechowywane w magazynie klucza musi być klucze hello tooread główną usługi Azure Active Directory zestaw toopermit hello. Ustaw uprawnienia na magazyn kluczy o [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a>Tworzenie maszyny wirtualnej
tootest hello proces szyfrowania, Utwórz Maszynę wirtualną. Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM* przy użyciu *systemu Windows Server 2016 Datacenter* obrazu:

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "mypublicdns$(Get-Random)"

$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$cred = Get-Credential

$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```


## <a name="encrypt-virtual-machine"></a>Szyfrowanie maszyny wirtualnej
dyski wirtualne hello tooencrypt, przełączeniem razem wszystkie poprzednie składniki hello:

1. Określ hello nazwy głównej usługi Azure Active Directory i hasło.
2. Określ hello Key Vault toostore hello metadanych dla zaszyfrowanych dysków.
3. Określ toouse kluczy kryptograficznych hello hello rzeczywiste szyfrowania i odszyfrowywania.
4. Określ, czy tooencrypt hello systemu operacyjnego, dysku dysków z danymi hello lub wszystkie.

Szyfrowanie maszyny Wirtualnej z [AzureRmVMDiskEncryptionExtension zestaw](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) przy użyciu klucza usługi Azure Key Vault hello i poświadczenia główne usługi Azure Active Directory. Witaj poniższy przykład pobiera wszystkie informacje o kluczu hello, a następnie szyfruje hello maszyny Wirtualnej o nazwie *myVM*:

```powershell
$keyVault = Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $rgName;
$diskEncryptionKeyVaultUrl = $keyVault.VaultUri;
$keyVaultResourceId = $keyVault.ResourceId;
$keyEncryptionKeyUrl = (Get-AzureKeyVaultKey -VaultName $keyVaultName -Name myKey).Key.kid;

Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $rgName `
    -VMName $vmName `
    -AadClientID $app.ApplicationId `
    -AadClientSecret $securePassword `
    -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl `
    -DiskEncryptionKeyVaultId $keyVaultResourceId `
    -KeyEncryptionKeyUrl $keyEncryptionKeyUrl `
    -KeyEncryptionKeyVaultId $keyVaultResourceId
```

Zaakceptuj hello toocontinue monitu hello szyfrowanie maszyny Wirtualnej. podczas procesu hello uruchamia ponownie Hello maszyny Wirtualnej. Po zakończeniu procesu szyfrowania hello i hello maszyny Wirtualnej został ponownie uruchomiony, przejrzyj hello stanu szyfrowania z [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

Witaj danych wyjściowych jest toohello podobnie poniższy przykład:

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać więcej informacji na temat zarządzania usługą Azure Key Vault, zobacz [Konfigurowanie magazynu kluczy dla maszyn wirtualnych](key-vault-setup.md).
* Aby uzyskać więcej informacji o szyfrowaniu dysków, takich jak przygotowywanie zaszyfrowanego niestandardowego wirtualna tooupload tooAzure, zobacz [szyfrowania dysków Azure](../../security/azure-security-disk-encryption.md).
