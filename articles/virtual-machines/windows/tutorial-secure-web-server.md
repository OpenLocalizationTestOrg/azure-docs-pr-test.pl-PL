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
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="ebde1-103">Zabezpieczenia serwera sieci web usług IIS z certyfikatów SSL na maszynie wirtualnej systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="ebde1-103">Secure IIS web server with SSL certificates on a Windows virtual machine in Azure</span></span>
<span data-ttu-id="ebde1-104">serwery sieci web toosecure, certyfikat później SSL (Secure Sockets) mogą być używane tooencrypt ruchu w sieci web.</span><span class="sxs-lookup"><span data-stu-id="ebde1-104">toosecure web servers, a Secure Sockets Later (SSL) certificate can be used tooencrypt web traffic.</span></span> <span data-ttu-id="ebde1-105">Te certyfikaty SSL mogą być przechowywane w usłudze Azure Key Vault i umożliwia bezpieczne wdrażanie certyfikatów tooWindows o maszynach wirtualnych (VM) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ebde1-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates tooWindows virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="ebde1-106">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="ebde1-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ebde1-107">Tworzenie usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="ebde1-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="ebde1-108">Generowanie lub Przekaż certyfikat toohello magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="ebde1-108">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="ebde1-109">Utwórz maszynę Wirtualną i zainstalowania serwera sieci web usług IIS hello</span><span class="sxs-lookup"><span data-stu-id="ebde1-109">Create a VM and install hello IIS web server</span></span>
> * <span data-ttu-id="ebde1-110">Wstaw hello certyfikatu do hello maszyny Wirtualnej i skonfiguruj program IIS wraz z powiązaniem SSL</span><span class="sxs-lookup"><span data-stu-id="ebde1-110">Inject hello certificate into hello VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="ebde1-111">Ten samouczek wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="ebde1-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="ebde1-112">Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="ebde1-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="ebde1-113">Jeśli potrzebujesz tooupgrade, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="ebde1-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="overview"></a><span data-ttu-id="ebde1-114">Omówienie</span><span class="sxs-lookup"><span data-stu-id="ebde1-114">Overview</span></span>
<span data-ttu-id="ebde1-115">Usługa Azure Key Vault zabezpiecza kluczy kryptograficznych i kluczy tajnych takich certyfikatów lub hasła.</span><span class="sxs-lookup"><span data-stu-id="ebde1-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="ebde1-116">Magazyn kluczy pozwala uprościć proces zarządzania hello certyfikatu i umożliwia toomaintain kontrolę nad kluczami, które uzyskują dostęp do tych certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="ebde1-116">Key Vault helps streamline hello certificate management process and enables you toomaintain control of keys that access those certificates.</span></span> <span data-ttu-id="ebde1-117">Można utworzyć certyfikatu z podpisem własnym wewnątrz usługi Key Vault, lub Przekaż istniejących, zaufanego certyfikatu, który już następującą.</span><span class="sxs-lookup"><span data-stu-id="ebde1-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="ebde1-118">Zamiast przy użyciu niestandardowego obrazu maszyny Wirtualnej, który zawiera certyfikaty rozszerzania w, wstrzyknąć certyfikatów do uruchomionej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ebde1-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="ebde1-119">Ten proces zapewnia, że certyfikaty aktualną hello są zainstalowane na serwerze sieci web podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="ebde1-119">This process ensures that hello most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="ebde1-120">Jeśli możesz odnowić lub zastąpić certyfikat, nie masz również toocreate nowego niestandardowego obrazu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ebde1-120">If you renew or replace a certificate, you don't also have toocreate a new custom VM image.</span></span> <span data-ttu-id="ebde1-121">Hello najnowsze certyfikaty są automatycznie dodane podczas tworzenia dodatkowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ebde1-121">hello latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="ebde1-122">W trakcie całego procesu hello certyfikaty hello nigdy nie pozostaw hello platformy Azure lub są widoczne w skrypcie, Historia wiersza polecenia lub szablonu.</span><span class="sxs-lookup"><span data-stu-id="ebde1-122">During hello whole process, hello certificates never leave hello Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="ebde1-123">Tworzenie usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="ebde1-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="ebde1-124">Przed utworzeniem magazyn kluczy i certyfikatów, Utwórz nową grupę zasobów o [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="ebde1-124">Before you can create a Key Vault and certificates, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="ebde1-125">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupSecureWeb* w hello *wschodnie stany USA* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="ebde1-125">hello following example creates a resource group named *myResourceGroupSecureWeb* in hello *East US* location:</span></span>

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

<span data-ttu-id="ebde1-126">Następnie należy utworzyć magazyn kluczy o [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span><span class="sxs-lookup"><span data-stu-id="ebde1-126">Next, create a Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span></span> <span data-ttu-id="ebde1-127">Każdy magazyn kluczy wymaga unikatowej nazwy i powinna być małe litery.</span><span class="sxs-lookup"><span data-stu-id="ebde1-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="ebde1-128">Zastąp `<mykeyvault>` w hello poniższy przykład z własną unikatową nazwę usługi Key Vault:</span><span class="sxs-lookup"><span data-stu-id="ebde1-128">Replace `<mykeyvault>` in hello following example with your own unique Key Vault name:</span></span>

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="ebde1-129">Wygeneruj certyfikat i przechowywania w magazynie kluczy</span><span class="sxs-lookup"><span data-stu-id="ebde1-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="ebde1-130">W środowisku produkcyjnym, należy zaimportować prawidłowy certyfikat podpisane przez zaufanego dostawcę z [AzureKeyVaultCertificate importu](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span><span class="sxs-lookup"><span data-stu-id="ebde1-130">For production use, you should import a valid certificate signed by trusted provider with [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span></span> <span data-ttu-id="ebde1-131">W tym samouczku hello poniższym przykładzie pokazano, jak można wygenerować certyfikatu z podpisem własnym z [AzureKeyVaultCertificate Dodaj](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) czy używa hello domyślne zasady dotyczące certyfikatów z [ Nowy AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span><span class="sxs-lookup"><span data-stu-id="ebde1-131">For this tutorial, hello following example shows how you can generate a self-signed certificate with [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) that uses hello default certificate policy from [New-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span></span> 

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


## <a name="create-a-virtual-machine"></a><span data-ttu-id="ebde1-132">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ebde1-132">Create a virtual machine</span></span>
<span data-ttu-id="ebde1-133">Zestaw administratora nazwę użytkownika i hasło dla maszyny Wirtualnej z hello [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="ebde1-133">Set an administrator username and password for hello VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="ebde1-134">Teraz możesz utworzyć maszynę Wirtualną za pomocą hello [AzureRmVM nowy](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="ebde1-134">Now you can create hello VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="ebde1-135">Witaj poniższy przykład tworzy hello wymagane składniki sieci wirtualnej, konfiguracja hello systemu operacyjnego, a następnie tworzy Maszynę wirtualną o nazwie *myVM*:</span><span class="sxs-lookup"><span data-stu-id="ebde1-135">hello following example creates hello required virtual network components, hello OS configuration, and then creates a VM named *myVM*:</span></span>

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

<span data-ttu-id="ebde1-136">Trwa kilka minut, aż hello toobe maszyny Wirtualnej utworzone.</span><span class="sxs-lookup"><span data-stu-id="ebde1-136">It takes a few minutes for hello VM toobe created.</span></span> <span data-ttu-id="ebde1-137">Witaj ostatniego kroku jest używana hello Azure niestandardowe rozszerzenie skryptu tooinstall powitania serwera sieci web IIS z [AzureRmVmExtension zestawu](/powershell/module/azurerm.compute/set-azurermvmextension).</span><span class="sxs-lookup"><span data-stu-id="ebde1-137">hello last step uses hello Azure Custom Script Extension tooinstall hello IIS web server with [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span></span>


## <a name="add-a-certificate-toovm-from-key-vault"></a><span data-ttu-id="ebde1-138">Dodaj tooVM certyfikatu z magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="ebde1-138">Add a certificate tooVM from Key Vault</span></span>
<span data-ttu-id="ebde1-139">tooadd hello certyfikat z magazynu kluczy tooa maszyny Wirtualnej, uzyskać identyfikator hello certyfikatu z [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="ebde1-139">tooadd hello certificate from Key Vault tooa VM, obtain hello ID of your certificate with [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span></span> <span data-ttu-id="ebde1-140">Dodaj hello certyfikatu toohello maszyny Wirtualnej z [AzureRmVMSecret Dodaj](/powershell/module/azurerm.compute/add-azurermvmsecret):</span><span class="sxs-lookup"><span data-stu-id="ebde1-140">Add hello certificate toohello VM with [Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span></span>

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-toouse-hello-certificate"></a><span data-ttu-id="ebde1-141">Konfigurowanie certyfikatu hello toouse usług IIS</span><span class="sxs-lookup"><span data-stu-id="ebde1-141">Configure IIS toouse hello certificate</span></span>
<span data-ttu-id="ebde1-142">Użyj hello niestandardowe rozszerzenie skryptu ponownie, podając [AzureRmVMExtension zestaw](/powershell/module/azurerm.compute/set-azurermvmextension) konfiguracji usług IIS hello tooupdate.</span><span class="sxs-lookup"><span data-stu-id="ebde1-142">Use hello Custom Script Extension again with [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooupdate hello IIS configuration.</span></span> <span data-ttu-id="ebde1-143">Ta aktualizacja dotyczy certyfikatu hello wprowadzonym z tooIIS magazyn kluczy i konfiguruje hello powiązanie sieci web:</span><span class="sxs-lookup"><span data-stu-id="ebde1-143">This update applies hello certificate injected from Key Vault tooIIS and configures hello web binding:</span></span>

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


### <a name="test-hello-secure-web-app"></a><span data-ttu-id="ebde1-144">Przetestuj aplikację sieci web bezpiecznego hello</span><span class="sxs-lookup"><span data-stu-id="ebde1-144">Test hello secure web app</span></span>
<span data-ttu-id="ebde1-145">Uzyskaj hello publicznego adresu IP maszyny Wirtualnej z [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="ebde1-145">Obtain hello public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="ebde1-146">Witaj poniższy przykład uzyskuje hello adres IP dla `myPublicIP` utworzony wcześniej:</span><span class="sxs-lookup"><span data-stu-id="ebde1-146">hello following example obtains hello IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="ebde1-147">Teraz możesz otworzyć przeglądarkę sieci web i wprowadź `https://<myPublicIP>` na pasku adresu hello.</span><span class="sxs-lookup"><span data-stu-id="ebde1-147">Now you can open a web browser and enter `https://<myPublicIP>` in hello address bar.</span></span> <span data-ttu-id="ebde1-148">Wybierz tooaccept hello ostrzeżenie o zabezpieczeniach Jeśli używasz certyfikatu z podpisem własnym, **szczegóły** , a następnie **przejdź na stronę sieci Web toohello**:</span><span class="sxs-lookup"><span data-stu-id="ebde1-148">tooaccept hello security warning if you used a self-signed certificate, select **Details** and then **Go on toohello webpage**:</span></span>

![Zaakceptuj ostrzeżenie o zabezpieczeniach przeglądarki sieci web](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="ebde1-150">Jak hello poniższy przykład następnie wyświetleniem zabezpieczonej witryny sieci Web usług IIS:</span><span class="sxs-lookup"><span data-stu-id="ebde1-150">Your secured IIS website is then displayed as in hello following example:</span></span>

![Widok działa bezpiecznej witryny usług IIS](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a><span data-ttu-id="ebde1-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ebde1-152">Next steps</span></span>

<span data-ttu-id="ebde1-153">W tym samouczku serwer sieci web usług IIS jest zabezpieczony za pomocą certyfikatu SSL, przechowywane w usłudze Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="ebde1-153">In this tutorial, you secured an IIS web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="ebde1-154">W tym samouczku omówiono:</span><span class="sxs-lookup"><span data-stu-id="ebde1-154">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ebde1-155">Tworzenie usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="ebde1-155">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="ebde1-156">Generowanie lub Przekaż certyfikat toohello magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="ebde1-156">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="ebde1-157">Utwórz maszynę Wirtualną i zainstalowania serwera sieci web usług IIS hello</span><span class="sxs-lookup"><span data-stu-id="ebde1-157">Create a VM and install hello IIS web server</span></span>
> * <span data-ttu-id="ebde1-158">Wstaw hello certyfikatu do hello maszyny Wirtualnej i skonfiguruj program IIS wraz z powiązaniem SSL</span><span class="sxs-lookup"><span data-stu-id="ebde1-158">Inject hello certificate into hello VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="ebde1-159">Postępuj zgodnie z tym toosee łącze wstępnie skompilowany przykłady skryptów maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ebde1-159">Follow this link toosee pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ebde1-160">Przykłady skryptów maszyny wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="ebde1-160">Windows virtual machine script samples</span></span>](./powershell-samples.md)