---
title: "Zabezpieczenie usług IIS z certyfikatów SSL na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zabezpieczyć serwer sieci web usług IIS z certyfikatów SSL na maszynie Wirtualnej systemu Windows na platformie Azure"
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
ms.openlocfilehash: 6567853e9ef3cad63595dc0afe7a793bdc5d972c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="85f09-103">Zabezpieczenia serwera sieci web usług IIS z certyfikatów SSL na maszynie wirtualnej systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="85f09-103">Secure IIS web server with SSL certificates on a Windows virtual machine in Azure</span></span>
<span data-ttu-id="85f09-104">Do zabezpieczania serwerów sieci web, certyfikatu później SSL (Secure Sockets) może być używany do szyfrowania ruchu w sieci web.</span><span class="sxs-lookup"><span data-stu-id="85f09-104">To secure web servers, a Secure Sockets Later (SSL) certificate can be used to encrypt web traffic.</span></span> <span data-ttu-id="85f09-105">Te certyfikaty SSL mogą być przechowywane w usłudze Azure Key Vault i Zezwalaj wdrożeń zabezpieczonych certyfikatów na maszynach wirtualnych systemu Windows (VM) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="85f09-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates to Windows virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="85f09-106">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="85f09-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="85f09-107">Tworzenie usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="85f09-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="85f09-108">Generowanie lub Przekaż certyfikat do magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="85f09-108">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="85f09-109">Utwórz maszynę Wirtualną i zainstaluj serwer sieci web usług IIS</span><span class="sxs-lookup"><span data-stu-id="85f09-109">Create a VM and install the IIS web server</span></span>
> * <span data-ttu-id="85f09-110">Wstaw certyfikat do maszyny Wirtualnej i skonfiguruj program IIS wraz z powiązaniem SSL</span><span class="sxs-lookup"><span data-stu-id="85f09-110">Inject the certificate into the VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="85f09-111">Dla tego samouczka jest wymagany moduł Azure PowerShell w wersji 3.6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="85f09-111">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="85f09-112">Uruchom polecenie ` Get-Module -ListAvailable AzureRM`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="85f09-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="85f09-113">Jeśli potrzebujesz do uaktualnienia, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="85f09-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="overview"></a><span data-ttu-id="85f09-114">Omówienie</span><span class="sxs-lookup"><span data-stu-id="85f09-114">Overview</span></span>
<span data-ttu-id="85f09-115">Usługa Azure Key Vault zabezpiecza kluczy kryptograficznych i kluczy tajnych takich certyfikatów lub hasła.</span><span class="sxs-lookup"><span data-stu-id="85f09-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="85f09-116">Key Vault ułatwia uprościć proces zarządzania certyfikatu i pozwala zachować kontrolę nad kluczami, które uzyskują dostęp do tych certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="85f09-116">Key Vault helps streamline the certificate management process and enables you to maintain control of keys that access those certificates.</span></span> <span data-ttu-id="85f09-117">Można utworzyć certyfikatu z podpisem własnym wewnątrz usługi Key Vault, lub Przekaż istniejących, zaufanego certyfikatu, który już następującą.</span><span class="sxs-lookup"><span data-stu-id="85f09-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="85f09-118">Zamiast przy użyciu niestandardowego obrazu maszyny Wirtualnej, który zawiera certyfikaty rozszerzania w, wstrzyknąć certyfikatów do uruchomionej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="85f09-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="85f09-119">Ten proces zapewnia, że najbardziej aktualne certyfikaty są zainstalowane na serwerze sieci web podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="85f09-119">This process ensures that the most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="85f09-120">Jeśli odnowić lub Zastąp certyfikat, masz nie można utworzyć nowego niestandardowego obrazu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="85f09-120">If you renew or replace a certificate, you don't also have to create a new custom VM image.</span></span> <span data-ttu-id="85f09-121">Najnowsze certyfikaty są automatycznie dodane podczas tworzenia dodatkowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="85f09-121">The latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="85f09-122">W trakcie całego nigdy nie certyfikatów pozostaw platformy Azure lub są widoczne w skrypcie, Historia wiersza polecenia lub szablonu.</span><span class="sxs-lookup"><span data-stu-id="85f09-122">During the whole process, the certificates never leave the Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="85f09-123">Tworzenie usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="85f09-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="85f09-124">Przed utworzeniem magazyn kluczy i certyfikatów, Utwórz nową grupę zasobów o [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="85f09-124">Before you can create a Key Vault and certificates, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="85f09-125">Poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupSecureWeb* w *wschodnie stany USA* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="85f09-125">The following example creates a resource group named *myResourceGroupSecureWeb* in the *East US* location:</span></span>

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

<span data-ttu-id="85f09-126">Następnie należy utworzyć magazyn kluczy o [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span><span class="sxs-lookup"><span data-stu-id="85f09-126">Next, create a Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span></span> <span data-ttu-id="85f09-127">Każdy magazyn kluczy wymaga unikatowej nazwy i powinna być małe litery.</span><span class="sxs-lookup"><span data-stu-id="85f09-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="85f09-128">Zastąp `<mykeyvault>` w poniższym przykładzie z własną unikatową nazwę usługi Key Vault:</span><span class="sxs-lookup"><span data-stu-id="85f09-128">Replace `<mykeyvault>` in the following example with your own unique Key Vault name:</span></span>

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="85f09-129">Wygeneruj certyfikat i przechowywania w magazynie kluczy</span><span class="sxs-lookup"><span data-stu-id="85f09-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="85f09-130">W środowisku produkcyjnym, należy zaimportować prawidłowy certyfikat podpisane przez zaufanego dostawcę z [AzureKeyVaultCertificate importu](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span><span class="sxs-lookup"><span data-stu-id="85f09-130">For production use, you should import a valid certificate signed by trusted provider with [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span></span> <span data-ttu-id="85f09-131">W tym samouczku, w poniższym przykładzie pokazano, jak można wygenerować certyfikatu z podpisem własnym z [AzureKeyVaultCertificate Dodaj](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) używającą domyślne zasady certyfikatów z [AzureKeyVaultCertificatePolicy nowy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span><span class="sxs-lookup"><span data-stu-id="85f09-131">For this tutorial, the following example shows how you can generate a self-signed certificate with [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) that uses the default certificate policy from [New-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span></span> 

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


## <a name="create-a-virtual-machine"></a><span data-ttu-id="85f09-132">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="85f09-132">Create a virtual machine</span></span>
<span data-ttu-id="85f09-133">Ustaw nazwę użytkownika i hasło administratora dla maszyny Wirtualnej z [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="85f09-133">Set an administrator username and password for the VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="85f09-134">Teraz możesz utworzyć maszynę Wirtualną z [AzureRmVM nowy](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="85f09-134">Now you can create the VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="85f09-135">Poniższy przykład tworzy składniki wymagane sieci wirtualnej, konfiguracja systemu operacyjnego, a następnie tworzy Maszynę wirtualną o nazwie *myVM*:</span><span class="sxs-lookup"><span data-stu-id="85f09-135">The following example creates the required virtual network components, the OS configuration, and then creates a VM named *myVM*:</span></span>

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

# Use the Custom Script Extension to install IIS
Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server -IncludeManagementTools"}'
```

<span data-ttu-id="85f09-136">Trwa kilka minut, aż do utworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="85f09-136">It takes a few minutes for the VM to be created.</span></span> <span data-ttu-id="85f09-137">Ostatnim krokiem używa niestandardowe rozszerzenie skryptu Azure w celu zainstalowania serwera sieci web usług IIS z [AzureRmVmExtension zestawu](/powershell/module/azurerm.compute/set-azurermvmextension).</span><span class="sxs-lookup"><span data-stu-id="85f09-137">The last step uses the Azure Custom Script Extension to install the IIS web server with [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span></span>


## <a name="add-a-certificate-to-vm-from-key-vault"></a><span data-ttu-id="85f09-138">Dodawanie certyfikatu do maszyny Wirtualnej z magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="85f09-138">Add a certificate to VM from Key Vault</span></span>
<span data-ttu-id="85f09-139">Aby dodać certyfikat z magazynu kluczy do maszyny Wirtualnej, należy uzyskać identyfikator certyfikatu z [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="85f09-139">To add the certificate from Key Vault to a VM, obtain the ID of your certificate with [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span></span> <span data-ttu-id="85f09-140">Dodawanie certyfikatu do maszyny Wirtualnej z [AzureRmVMSecret Dodaj](/powershell/module/azurerm.compute/add-azurermvmsecret):</span><span class="sxs-lookup"><span data-stu-id="85f09-140">Add the certificate to the VM with [Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span></span>

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-to-use-the-certificate"></a><span data-ttu-id="85f09-141">Konfigurowanie usług IIS do używania certyfikatu</span><span class="sxs-lookup"><span data-stu-id="85f09-141">Configure IIS to use the certificate</span></span>
<span data-ttu-id="85f09-142">Niestandardowe rozszerzenie skryptu ponownie, podając [AzureRmVMExtension zestaw](/powershell/module/azurerm.compute/set-azurermvmextension) można zaktualizować konfiguracji usług IIS.</span><span class="sxs-lookup"><span data-stu-id="85f09-142">Use the Custom Script Extension again with [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) to update the IIS configuration.</span></span> <span data-ttu-id="85f09-143">Ta aktualizacja dotyczy certyfikatu wprowadzonym z magazynu kluczy usług IIS i konfiguruje powiązanie sieci web:</span><span class="sxs-lookup"><span data-stu-id="85f09-143">This update applies the certificate injected from Key Vault to IIS and configures the web binding:</span></span>

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


### <a name="test-the-secure-web-app"></a><span data-ttu-id="85f09-144">Testowanie aplikacji sieci web bezpieczne</span><span class="sxs-lookup"><span data-stu-id="85f09-144">Test the secure web app</span></span>
<span data-ttu-id="85f09-145">Publiczny adres IP maszyny wirtualnej z [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="85f09-145">Obtain the public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="85f09-146">Poniższy przykład uzyskuje adres IP dla `myPublicIP` utworzony wcześniej:</span><span class="sxs-lookup"><span data-stu-id="85f09-146">The following example obtains the IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="85f09-147">Teraz możesz otworzyć przeglądarkę sieci web i wprowadź `https://<myPublicIP>` na pasku adresu.</span><span class="sxs-lookup"><span data-stu-id="85f09-147">Now you can open a web browser and enter `https://<myPublicIP>` in the address bar.</span></span> <span data-ttu-id="85f09-148">Aby zaakceptować zabezpieczeń ostrzeżenie, jeśli używasz certyfikatu z podpisem własnym, wybierz **szczegóły** , a następnie **przejdź do strony sieci Web**:</span><span class="sxs-lookup"><span data-stu-id="85f09-148">To accept the security warning if you used a self-signed certificate, select **Details** and then **Go on to the webpage**:</span></span>

![Zaakceptuj ostrzeżenie o zabezpieczeniach przeglądarki sieci web](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="85f09-150">Wyświetlane są następnie zabezpieczonej witryny sieci Web usług IIS, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="85f09-150">Your secured IIS website is then displayed as in the following example:</span></span>

![Widok działa bezpiecznej witryny usług IIS](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a><span data-ttu-id="85f09-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="85f09-152">Next steps</span></span>

<span data-ttu-id="85f09-153">W tym samouczku serwer sieci web usług IIS jest zabezpieczony za pomocą certyfikatu SSL, przechowywane w usłudze Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="85f09-153">In this tutorial, you secured an IIS web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="85f09-154">Możesz przedstawiono sposób do:</span><span class="sxs-lookup"><span data-stu-id="85f09-154">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="85f09-155">Tworzenie usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="85f09-155">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="85f09-156">Generowanie lub Przekaż certyfikat do magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="85f09-156">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="85f09-157">Utwórz maszynę Wirtualną i zainstaluj serwer sieci web usług IIS</span><span class="sxs-lookup"><span data-stu-id="85f09-157">Create a VM and install the IIS web server</span></span>
> * <span data-ttu-id="85f09-158">Wstaw certyfikat do maszyny Wirtualnej i skonfiguruj program IIS wraz z powiązaniem SSL</span><span class="sxs-lookup"><span data-stu-id="85f09-158">Inject the certificate into the VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="85f09-159">Wykonaj to łącze, aby wyświetlić przykłady skryptów wbudowanych maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="85f09-159">Follow this link to see pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="85f09-160">Przykłady skryptów maszyny wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="85f09-160">Windows virtual machine script samples</span></span>](./powershell-samples.md)