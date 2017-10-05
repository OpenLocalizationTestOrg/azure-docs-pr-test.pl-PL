---
title: "Szyfrowanie dysków na maszynie Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: "Jak zaszyfrować dyski wirtualne na maszynie Wirtualnej systemu Windows, aby zwiększyć bezpieczeństwo, przy użyciu programu Azure PowerShell"
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
ms.openlocfilehash: 98b42b252a601af090579e3939f3c7ab91c3803b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-encrypt-virtual-disks-on-a-windows-vm"></a><span data-ttu-id="c650c-103">Jak zaszyfrować dyski wirtualne na maszynie Wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c650c-103">How to encrypt virtual disks on a Windows VM</span></span>
<span data-ttu-id="c650c-104">Ulepszone maszyny wirtualnej (VM) zabezpieczeń i zgodności mogą być szyfrowane dyski wirtualne na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c650c-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="c650c-105">Dyski są szyfrowane za pomocą kluczy kryptograficznych, które są już zabezpieczone w usłudze Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c650c-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="c650c-106">Kontrolowanie tych kluczy kryptograficznych i przeprowadzić inspekcję ich używania.</span><span class="sxs-lookup"><span data-stu-id="c650c-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="c650c-107">Ten artykuł zawiera szczegóły dotyczące sposobu szyfrowania dysków wirtualnych w maszynie Wirtualnej z systemem Windows przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c650c-107">This article details how to encrypt virtual disks on a Windows VM using Azure PowerShell.</span></span> <span data-ttu-id="c650c-108">Możesz również [szyfrowania maszyny Wirtualnej systemu Linux przy użyciu programu Azure CLI 2.0](../linux/encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="c650c-108">You can also [encrypt a Linux VM using the Azure CLI 2.0](../linux/encrypt-disks.md).</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="c650c-109">Omówienie szyfrowania dysków</span><span class="sxs-lookup"><span data-stu-id="c650c-109">Overview of disk encryption</span></span>
<span data-ttu-id="c650c-110">Dyski wirtualne na maszynach wirtualnych systemu Windows są szyfrowane, gdy za pomocą funkcji Bitlocker.</span><span class="sxs-lookup"><span data-stu-id="c650c-110">Virtual disks on Windows VMs are encrypted at rest using Bitlocker.</span></span> <span data-ttu-id="c650c-111">Jest bezpłatna dla szyfrowania dysków wirtualnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c650c-111">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="c650c-112">Klucze szyfrowania są przechowywane w usługi Azure Key Vault przy użyciu ochrony oprogramowania, lub możesz zaimportować lub wygenerować klucze w sprzętowych modułach zabezpieczeń (HSM) certyfikowane do FIPS 140-2 poziom 2 standardów.</span><span class="sxs-lookup"><span data-stu-id="c650c-112">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified to FIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="c650c-113">Te klucze szyfrowania są używane do szyfrowania i odszyfrowywania wirtualnych dysków dołączonych do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c650c-113">These cryptographic keys are used to encrypt and decrypt virtual disks attached to your VM.</span></span> <span data-ttu-id="c650c-114">Zachowanie kontroli nad tych kluczy kryptograficznych i przeprowadzić inspekcję ich używania.</span><span class="sxs-lookup"><span data-stu-id="c650c-114">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="c650c-115">Nazwy głównej usługi Azure Active Directory zapewnia mechanizm bezpiecznego do wystawiania tych kluczy kryptograficznych, ponieważ maszyny wirtualne są zasilane i wyłączanie.</span><span class="sxs-lookup"><span data-stu-id="c650c-115">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="c650c-116">Proces szyfrowania maszyny Wirtualnej jest następujący:</span><span class="sxs-lookup"><span data-stu-id="c650c-116">The process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="c650c-117">Tworzenie klucza kryptograficznego w usłudze Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c650c-117">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="c650c-118">Skonfiguruj klucza kryptograficznego, który może być używany do szyfrowania dysków.</span><span class="sxs-lookup"><span data-stu-id="c650c-118">Configure the cryptographic key to be usable for encrypting disks.</span></span>
3. <span data-ttu-id="c650c-119">Aby odczytać klucza kryptograficznego z usługi Azure Key Vault, utworzyć usługę Azure Active Directory podmiot z odpowiednimi uprawnieniami.</span><span class="sxs-lookup"><span data-stu-id="c650c-119">To read the cryptographic key from the Azure Key Vault, create an Azure Active Directory service principal with the appropriate permissions.</span></span>
4. <span data-ttu-id="c650c-120">Wydaj polecenie wirtualnych dysków, określając usługi Azure Active Directory usługa podmiotu zabezpieczeń i odpowiednie klucza kryptograficznego używanego do szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="c650c-120">Issue the command to encrypt your virtual disks, specifying the Azure Active Directory service principal and appropriate cryptographic key to be used.</span></span>
5. <span data-ttu-id="c650c-121">Nazwy głównej usługi Azure Active Directory żądań wymaganego klucza kryptograficznego z usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c650c-121">The Azure Active Directory service principal requests the required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="c650c-122">Dyski wirtualne są szyfrowane za pomocą podanego klucza kryptograficznego.</span><span class="sxs-lookup"><span data-stu-id="c650c-122">The virtual disks are encrypted using the provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="c650c-123">Proces szyfrowania</span><span class="sxs-lookup"><span data-stu-id="c650c-123">Encryption process</span></span>
<span data-ttu-id="c650c-124">Szyfrowanie dysków opiera się na następujące dodatkowe składniki:</span><span class="sxs-lookup"><span data-stu-id="c650c-124">Disk encryption relies on the following additional components:</span></span>

* <span data-ttu-id="c650c-125">**Usługa Azure Key Vault** — używane do ochrony kluczy kryptograficznych i kluczy tajnych używanych przez proces szyfrowania i odszyfrowywania dysku.</span><span class="sxs-lookup"><span data-stu-id="c650c-125">**Azure Key Vault** - used to safeguard cryptographic keys and secrets used for the disk encryption/decryption process.</span></span> 
  * <span data-ttu-id="c650c-126">Jeśli istnieje, można użyć istniejącego magazynu kluczy Azure.</span><span class="sxs-lookup"><span data-stu-id="c650c-126">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="c650c-127">Nie trzeba przeznaczyć magazyn kluczy szyfrowania dysków.</span><span class="sxs-lookup"><span data-stu-id="c650c-127">You do not have to dedicate a Key Vault to encrypting disks.</span></span>
  * <span data-ttu-id="c650c-128">Aby rozdzielić granice administracyjne i widoczności klucza, możesz utworzyć dedykowany magazyn kluczy.</span><span class="sxs-lookup"><span data-stu-id="c650c-128">To separate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="c650c-129">**Usługa Azure Active Directory** — obsługuje bezpiecznej wymiany wymagane klucze szyfrowania i uwierzytelniania dla żądanej akcji.</span><span class="sxs-lookup"><span data-stu-id="c650c-129">**Azure Active Directory** - handles the secure exchanging of required cryptographic keys and authentication for requested actions.</span></span> 
  * <span data-ttu-id="c650c-130">Zazwyczaj można użyć istniejącego wystąpienia usługi Azure Active Directory, do przechowywania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c650c-130">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="c650c-131">Nazwy głównej usługi zapewnia mechanizm bezpiecznego do żądania i wydawane odpowiednich kluczy kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="c650c-131">The service principal provides a secure mechanism to request and be issued the appropriate cryptographic keys.</span></span> <span data-ttu-id="c650c-132">Nie opracowujesz aplikację rzeczywista, która integruje się z usługą Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c650c-132">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="c650c-133">Wymagania i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="c650c-133">Requirements and limitations</span></span>
<span data-ttu-id="c650c-134">Obsługiwane scenariusze i wymagania dotyczące szyfrowania dysków:</span><span class="sxs-lookup"><span data-stu-id="c650c-134">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="c650c-135">Włączenie szyfrowania na nowych maszyn wirtualnych systemu Windows z portalu Azure Marketplace obrazy lub niestandardowego obrazu wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="c650c-135">Enabling encryption on new Windows VMs from Azure Marketplace images or custom VHD image.</span></span>
* <span data-ttu-id="c650c-136">Włączenie szyfrowania na istniejących maszyn wirtualnych systemu Windows na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c650c-136">Enabling encryption on existing Windows VMs in Azure.</span></span>
* <span data-ttu-id="c650c-137">Włączenie szyfrowania na maszynach wirtualnych systemu Windows, które są skonfigurowane przy użyciu funkcji miejsca do magazynowania.</span><span class="sxs-lookup"><span data-stu-id="c650c-137">Enabling encryption on Windows VMs that are configured using Storage Spaces.</span></span>
* <span data-ttu-id="c650c-138">Wyłączenie szyfrowania systemu operacyjnego i danych dyski dla maszyn wirtualnych systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="c650c-138">Disabling encryption on OS and data drives for Windows VMs.</span></span>
* <span data-ttu-id="c650c-139">Wszystkie zasoby (na przykład usługi Key Vault, konta magazynu i maszyny Wirtualnej) muszą być w tym samym regionie Azure i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c650c-139">All resources (such as Key Vault, Storage account, and VM) must be in the same Azure region and subscription.</span></span>
* <span data-ttu-id="c650c-140">Warstwy standardowa maszyn wirtualnych, takie jak, D, DS, G i GS serii maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c650c-140">Standard tier VMs, such as A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="c650c-141">Szyfrowanie dysku nie jest obecnie obsługiwane w następujących scenariuszach:</span><span class="sxs-lookup"><span data-stu-id="c650c-141">Disk encryption is not currently supported in the following scenarios:</span></span>

* <span data-ttu-id="c650c-142">Maszyny wirtualne warstwy podstawowa.</span><span class="sxs-lookup"><span data-stu-id="c650c-142">Basic tier VMs.</span></span>
* <span data-ttu-id="c650c-143">Maszyny wirtualne utworzone przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="c650c-143">VMs created using the Classic deployment model.</span></span>
* <span data-ttu-id="c650c-144">Aktualizowanie kluczy kryptograficznych w przypadku już zaszyfrowany maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c650c-144">Updating the cryptographic keys on an already encrypted VM.</span></span>
* <span data-ttu-id="c650c-145">Integracja z usługą zarządzania kluczami lokalnego.</span><span class="sxs-lookup"><span data-stu-id="c650c-145">Integration with on-prem Key Management Service.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="c650c-146">Tworzenie usługi Azure Key Vault i kluczy</span><span class="sxs-lookup"><span data-stu-id="c650c-146">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="c650c-147">Przed rozpoczęciem upewnij się, że masz zainstalowaną najnowszą wersję modułu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c650c-147">Before you start, make sure that the latest version of the Azure PowerShell module has been installed.</span></span> <span data-ttu-id="c650c-148">Aby uzyskać więcej informacji, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c650c-148">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="c650c-149">W przykładach poleceń Zastąp wszystkie parametry przykład własne nazwy, lokalizacji i wartości klucza.</span><span class="sxs-lookup"><span data-stu-id="c650c-149">Throughout the command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="c650c-150">W poniższych przykładach użyto Konwencji *myResourceGroup*, *myKeyVault*, *myVM*itp.</span><span class="sxs-lookup"><span data-stu-id="c650c-150">The following examples use a convention of *myResourceGroup*, *myKeyVault*, *myVM*, etc.</span></span>

<span data-ttu-id="c650c-151">Pierwszym krokiem jest do utworzenia magazynu kluczy Azure do przechowywania kluczy kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="c650c-151">The first step is to create an Azure Key Vault to store your cryptographic keys.</span></span> <span data-ttu-id="c650c-152">Usługa Azure Key Vault można przechowywać kluczy, kluczy tajnych lub haseł, które umożliwiają bezpieczne wdrożenie ich w aplikacji i usług.</span><span class="sxs-lookup"><span data-stu-id="c650c-152">Azure Key Vault can store keys, secrets, or passwords that allow you to securely implement them in your applications and services.</span></span> <span data-ttu-id="c650c-153">Szyfrowanie dysków wirtualnych można utworzyć magazyn kluczy do przechowywania klucza kryptograficznego, który jest używany do szyfrowania lub odszyfrowywania wirtualnych dysków.</span><span class="sxs-lookup"><span data-stu-id="c650c-153">For virtual disk encryption, you create a Key Vault to store a cryptographic key that is used to encrypt or decrypt your virtual disks.</span></span> 

<span data-ttu-id="c650c-154">Włącz dostawcy usługi Azure Key Vault w ramach Twojej subskrypcji platformy Azure z [AzureRmResourceProvider rejestru](/powershell/module/azurerm.resources/register-azurermresourceprovider), następnie utwórz nową grupę zasobów o [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="c650c-154">Enable the Azure Key Vault provider within your Azure subscription with [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), then create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="c650c-155">Poniższy przykład tworzy nazwę grupy zasobów *myResourceGroup* w *wschodnie stany USA* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="c650c-155">The following example creates a resource group name *myResourceGroup* in the *East US* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

<span data-ttu-id="c650c-156">Usługa Azure Key Vault zawierający klucze kryptograficzne i zasoby obliczeniowe skojarzone, takie jak magazyn i samej maszyny Wirtualnej musi znajdować się w tym samym regionie.</span><span class="sxs-lookup"><span data-stu-id="c650c-156">The Azure Key Vault containing the cryptographic keys and associated compute resources such as storage and the VM itself must reside in the same region.</span></span> <span data-ttu-id="c650c-157">Tworzenie usługi Azure Key Vault z [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) i włączyć usługi Key Vault służących do szyfrowania dysku.</span><span class="sxs-lookup"><span data-stu-id="c650c-157">Create an Azure Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) and enable the Key Vault for use with disk encryption.</span></span> <span data-ttu-id="c650c-158">Określ unikatową nazwę usługi Key Vault *keyVaultName* w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c650c-158">Specify a unique Key Vault name for *keyVaultName* as follows:</span></span>

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

<span data-ttu-id="c650c-159">Mogą być przechowywane przy użyciu oprogramowania lub sprzętu modelu zabezpieczeń (HSM) ochronę kluczy kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="c650c-159">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="c650c-160">Użycie modułów HSM wymaga premium magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="c650c-160">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="c650c-161">Brak dodatkowych kosztów tworzenia premium magazynu kluczy, a nie standardowy magazyn kluczy, którego przechowuje klucze chronione przez oprogramowanie.</span><span class="sxs-lookup"><span data-stu-id="c650c-161">There is an additional cost to creating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="c650c-162">Aby utworzyć premium magazynu kluczy, w poprzednim kroku Dodaj *- Sku "Premium"* parametrów.</span><span class="sxs-lookup"><span data-stu-id="c650c-162">To create a premium Key Vault, in the preceding step add the *-Sku "Premium"* parameters.</span></span> <span data-ttu-id="c650c-163">W poniższym przykładzie użyto klucze chronione przez oprogramowanie, ponieważ utworzono standardowe magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="c650c-163">The following example uses software-protected keys since we created a standard Key Vault.</span></span> 

<span data-ttu-id="c650c-164">W przypadku obu modeli ochrony platformy Azure musi otrzymać dostęp do żądania kluczy kryptograficznych, podczas rozruchu maszyny Wirtualnej do odszyfrowania dysków wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c650c-164">For both protection models, the Azure platform needs to be granted access to request the cryptographic keys when the VM boots to decrypt the virtual disks.</span></span> <span data-ttu-id="c650c-165">Tworzenie klucza kryptograficznego w magazyn kluczy o [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span><span class="sxs-lookup"><span data-stu-id="c650c-165">Create a cryptographic key in your Key Vault with [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span></span> <span data-ttu-id="c650c-166">W poniższym przykładzie jest tworzony klucz o nazwie *klucze*:</span><span class="sxs-lookup"><span data-stu-id="c650c-166">The following example creates a key named *myKey*:</span></span>

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-the-azure-active-directory-service-principal"></a><span data-ttu-id="c650c-167">Tworzenie nazwy głównej usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c650c-167">Create the Azure Active Directory service principal</span></span>
<span data-ttu-id="c650c-168">Podczas dyski wirtualne są zaszyfrowanie lub odszyfrowanie, należy określić konto w celu obsługi uwierzytelniania i wymiany kluczy kryptograficznych z magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="c650c-168">When virtual disks are encrypted or decrypted, you specify an account to handle the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="c650c-169">To konto, nazwy głównej usługi Azure Active Directory umożliwia platformy Azure zażądać odpowiednich kluczy kryptograficznych w imieniu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c650c-169">This account, an Azure Active Directory service principal, allows the Azure platform to request the appropriate cryptographic keys on behalf of the VM.</span></span> <span data-ttu-id="c650c-170">Domyślne wystąpienie usługi Azure Active Directory jest dostępne w Twojej subskrypcji, chociaż w wielu organizacjach są wyposażone w dedykowane katalogów usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c650c-170">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="c650c-171">Tworzenie nazwy głównej usługi w usłudze Azure Active Directory z [AzureRmADServicePrincipal nowy](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span><span class="sxs-lookup"><span data-stu-id="c650c-171">Create a service principal in Azure Active Directory with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span></span> <span data-ttu-id="c650c-172">Aby określić bezpieczne hasło, wykonaj [ograniczenia w usłudze Azure Active Directory i zasadami haseł](../../active-directory/active-directory-passwords-policy.md):</span><span class="sxs-lookup"><span data-stu-id="c650c-172">To specify a secure password, follow the [Password policies and restrictions in Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):</span></span>

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

<span data-ttu-id="c650c-173">Pomyślnie szyfrowania lub odszyfrowywania dysków wirtualnych, uprawnienia do klucza kryptograficznego, przechowywane w magazynie klucz musi mieć ustawioną zezwolenie na nazwę główną usługi Azure Active Directory do odczytu kluczy.</span><span class="sxs-lookup"><span data-stu-id="c650c-173">To successfully encrypt or decrypt virtual disks, permissions on the cryptographic key stored in Key Vault must be set to permit the Azure Active Directory service principal to read the keys.</span></span> <span data-ttu-id="c650c-174">Ustaw uprawnienia na magazyn kluczy o [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span><span class="sxs-lookup"><span data-stu-id="c650c-174">Set permissions on your Key Vault with [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a><span data-ttu-id="c650c-175">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c650c-175">Create virtual machine</span></span>
<span data-ttu-id="c650c-176">Aby przetestować proces szyfrowania, umożliwia tworzenie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c650c-176">To test the encryption process, let's create a VM.</span></span> <span data-ttu-id="c650c-177">Poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM* przy użyciu *systemu Windows Server 2016 Datacenter* obrazu:</span><span class="sxs-lookup"><span data-stu-id="c650c-177">The following example creates a VM named *myVM* using a *Windows Server 2016 Datacenter* image:</span></span>

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


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="c650c-178">Szyfrowanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c650c-178">Encrypt virtual machine</span></span>
<span data-ttu-id="c650c-179">Do szyfrowania dysków wirtualnych, można przenosić ze sobą wszystkie poprzednie składniki:</span><span class="sxs-lookup"><span data-stu-id="c650c-179">To encrypt the virtual disks, you bring together all the previous components:</span></span>

1. <span data-ttu-id="c650c-180">Podaj nazwę główną usługi Azure Active Directory i hasło.</span><span class="sxs-lookup"><span data-stu-id="c650c-180">Specify the Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="c650c-181">Określ Key Vault w celu przechowywania metadanych dla zaszyfrowanych dysków.</span><span class="sxs-lookup"><span data-stu-id="c650c-181">Specify the Key Vault to store the metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="c650c-182">Określ klucze kryptograficzne służące do rzeczywistego szyfrowania i odszyfrowywania.</span><span class="sxs-lookup"><span data-stu-id="c650c-182">Specify the cryptographic keys to use for the actual encryption and decryption.</span></span>
4. <span data-ttu-id="c650c-183">Określ, czy chcesz zaszyfrować dysk systemu operacyjnego, dyski danych lub all.</span><span class="sxs-lookup"><span data-stu-id="c650c-183">Specify whether you want to encrypt the OS disk, the data disks, or all.</span></span>

<span data-ttu-id="c650c-184">Szyfrowanie maszyny Wirtualnej z [AzureRmVMDiskEncryptionExtension zestaw](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) przy użyciu klucza usługi Azure Key Vault i poświadczenia główne usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c650c-184">Encrypt your VM with [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) using the Azure Key Vault key and Azure Active Directory service principal credentials.</span></span> <span data-ttu-id="c650c-185">Poniższy przykład pobiera wszystkie informacje o kluczu, a następnie szyfruje maszyny Wirtualnej o nazwie *myVM*:</span><span class="sxs-lookup"><span data-stu-id="c650c-185">The following example retrieves all the key information then encrypts the VM named *myVM*:</span></span>

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

<span data-ttu-id="c650c-186">Zaakceptować monit o kontynuowanie szyfrowania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c650c-186">Accept the prompt to continue with the VM encryption.</span></span> <span data-ttu-id="c650c-187">Podczas procesu ponownego uruchomienia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c650c-187">The VM restarts during the process.</span></span> <span data-ttu-id="c650c-188">Po zakończeniu procesu szyfrowania i uruchomieniu maszyny Wirtualnej, przejrzyj stanu szyfrowania z [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span><span class="sxs-lookup"><span data-stu-id="c650c-188">Once the encryption process completes and the VM has rebooted, review the encryption status with [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span></span>

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

<span data-ttu-id="c650c-189">Dane wyjściowe są podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="c650c-189">The output is similar to the following example:</span></span>

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a><span data-ttu-id="c650c-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c650c-190">Next steps</span></span>
* <span data-ttu-id="c650c-191">Aby uzyskać więcej informacji na temat zarządzania usługą Azure Key Vault, zobacz [Konfigurowanie magazynu kluczy dla maszyn wirtualnych](key-vault-setup.md).</span><span class="sxs-lookup"><span data-stu-id="c650c-191">For more information about managing Azure Key Vault, see [Set up Key Vault for virtual machines](key-vault-setup.md).</span></span>
* <span data-ttu-id="c650c-192">Aby uzyskać więcej informacji o szyfrowaniu dysków, takich jak przygotowywanie zaszyfrowanego niestandardowego maszyny Wirtualnej do przekazania do platformy Azure, zobacz [szyfrowania dysków Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="c650c-192">For more information about disk encryption, such as preparing an encrypted custom VM to upload to Azure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
