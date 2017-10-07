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
# <a name="how-tooencrypt-virtual-disks-on-a-windows-vm"></a><span data-ttu-id="e5346-103">Jak tooencrypt dyski wirtualne na maszynie Wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="e5346-103">How tooencrypt virtual disks on a Windows VM</span></span>
<span data-ttu-id="e5346-104">Ulepszone maszyny wirtualnej (VM) zabezpieczeń i zgodności mogą być szyfrowane dyski wirtualne na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e5346-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="e5346-105">Dyski są szyfrowane za pomocą kluczy kryptograficznych, które są już zabezpieczone w usłudze Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e5346-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="e5346-106">Kontrolowanie tych kluczy kryptograficznych i przeprowadzić inspekcję ich używania.</span><span class="sxs-lookup"><span data-stu-id="e5346-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="e5346-107">Ten sposób artykuł szczegóły tooencrypt dyski wirtualne na maszynie Wirtualnej z systemem Windows przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e5346-107">This article details how tooencrypt virtual disks on a Windows VM using Azure PowerShell.</span></span> <span data-ttu-id="e5346-108">Możesz również [szyfrowania maszyny Wirtualnej systemu Linux przy użyciu hello Azure CLI 2.0](../linux/encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="e5346-108">You can also [encrypt a Linux VM using hello Azure CLI 2.0](../linux/encrypt-disks.md).</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="e5346-109">Omówienie szyfrowania dysków</span><span class="sxs-lookup"><span data-stu-id="e5346-109">Overview of disk encryption</span></span>
<span data-ttu-id="e5346-110">Dyski wirtualne na maszynach wirtualnych systemu Windows są szyfrowane, gdy za pomocą funkcji Bitlocker.</span><span class="sxs-lookup"><span data-stu-id="e5346-110">Virtual disks on Windows VMs are encrypted at rest using Bitlocker.</span></span> <span data-ttu-id="e5346-111">Jest bezpłatna dla szyfrowania dysków wirtualnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e5346-111">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="e5346-112">Klucze szyfrowania są przechowywane w usługi Azure Key Vault przy użyciu ochrony oprogramowania, lub możesz zaimportować lub wygenerować klucze w sprzętowych modułach zabezpieczeń (HSM) certyfikowane tooFIPS 140-2 poziom 2 standardów.</span><span class="sxs-lookup"><span data-stu-id="e5346-112">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="e5346-113">Te klucze szyfrowania są używane tooencrypt i odszyfrowywania tooyour dołączonych dysków wirtualnych maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5346-113">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="e5346-114">Zachowanie kontroli nad tych kluczy kryptograficznych i przeprowadzić inspekcję ich używania.</span><span class="sxs-lookup"><span data-stu-id="e5346-114">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="e5346-115">Nazwy głównej usługi Azure Active Directory zapewnia mechanizm bezpiecznego do wystawiania tych kluczy kryptograficznych, ponieważ maszyny wirtualne są zasilane i wyłączanie.</span><span class="sxs-lookup"><span data-stu-id="e5346-115">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="e5346-116">proces Hello szyfrowania maszyny Wirtualnej przebiega w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e5346-116">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="e5346-117">Tworzenie klucza kryptograficznego w usłudze Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e5346-117">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="e5346-118">Skonfiguruj hello kryptograficznych klucza toobe można używać do szyfrowania dysków.</span><span class="sxs-lookup"><span data-stu-id="e5346-118">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="e5346-119">klucz kryptograficzny hello tooread z hello Azure Key Vault, Utwórz usługę Azure Active Directory podmiotu zabezpieczeń z odpowiednimi uprawnieniami hello.</span><span class="sxs-lookup"><span data-stu-id="e5346-119">tooread hello cryptographic key from hello Azure Key Vault, create an Azure Active Directory service principal with hello appropriate permissions.</span></span>
4. <span data-ttu-id="e5346-120">Wystawiać tooencrypt polecenia hello wirtualnych dysków, określenie nazwy głównej usługi Azure Active Directory hello i odpowiednie toobe klucza kryptograficznego używane.</span><span class="sxs-lookup"><span data-stu-id="e5346-120">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory service principal and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="e5346-121">główne żądania usługi Azure Active Directory Hello hello wymaganego klucza kryptograficznego z usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e5346-121">hello Azure Active Directory service principal requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="e5346-122">dyski wirtualne Hello są szyfrowane za pomocą klucza kryptograficznego hello podane.</span><span class="sxs-lookup"><span data-stu-id="e5346-122">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="e5346-123">Proces szyfrowania</span><span class="sxs-lookup"><span data-stu-id="e5346-123">Encryption process</span></span>
<span data-ttu-id="e5346-124">Szyfrowanie dysków opiera się na powitania następujące dodatkowe składniki:</span><span class="sxs-lookup"><span data-stu-id="e5346-124">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="e5346-125">**Usługa Azure Key Vault** — używane toosafeguard kluczy kryptograficznych i kluczy tajnych używane podczas procesu szyfrowania i odszyfrowywania dysku hello.</span><span class="sxs-lookup"><span data-stu-id="e5346-125">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span> 
  * <span data-ttu-id="e5346-126">Jeśli istnieje, można użyć istniejącego magazynu kluczy Azure.</span><span class="sxs-lookup"><span data-stu-id="e5346-126">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="e5346-127">Nie masz toodedicate dysków tooencrypting magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="e5346-127">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="e5346-128">granice administracyjne tooseparate i widoczności klucza, można utworzyć dedykowane Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e5346-128">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="e5346-129">**Usługa Azure Active Directory** — Witaj uchwytów bezpiecznej wymiany kluczy kryptograficznych wymagane i uwierzytelniania dla żądanej akcji.</span><span class="sxs-lookup"><span data-stu-id="e5346-129">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span> 
  * <span data-ttu-id="e5346-130">Zazwyczaj można użyć istniejącego wystąpienia usługi Azure Active Directory, do przechowywania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e5346-130">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="e5346-131">nazwy głównej usługi Hello zapewnia toorequest mechanizmu bezpiecznego i wydawane hello odpowiednich kluczy kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="e5346-131">hello service principal provides a secure mechanism toorequest and be issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="e5346-132">Nie opracowujesz aplikację rzeczywista, która integruje się z usługą Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e5346-132">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="e5346-133">Wymagania i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="e5346-133">Requirements and limitations</span></span>
<span data-ttu-id="e5346-134">Obsługiwane scenariusze i wymagania dotyczące szyfrowania dysków:</span><span class="sxs-lookup"><span data-stu-id="e5346-134">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="e5346-135">Włączenie szyfrowania na nowych maszyn wirtualnych systemu Windows z portalu Azure Marketplace obrazy lub niestandardowego obrazu wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="e5346-135">Enabling encryption on new Windows VMs from Azure Marketplace images or custom VHD image.</span></span>
* <span data-ttu-id="e5346-136">Włączenie szyfrowania na istniejących maszyn wirtualnych systemu Windows na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e5346-136">Enabling encryption on existing Windows VMs in Azure.</span></span>
* <span data-ttu-id="e5346-137">Włączenie szyfrowania na maszynach wirtualnych systemu Windows, które są skonfigurowane przy użyciu funkcji miejsca do magazynowania.</span><span class="sxs-lookup"><span data-stu-id="e5346-137">Enabling encryption on Windows VMs that are configured using Storage Spaces.</span></span>
* <span data-ttu-id="e5346-138">Wyłączenie szyfrowania systemu operacyjnego i danych dyski dla maszyn wirtualnych systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="e5346-138">Disabling encryption on OS and data drives for Windows VMs.</span></span>
* <span data-ttu-id="e5346-139">Wszystkie zasoby (na przykład usługi Key Vault, konta magazynu i maszyny Wirtualnej) musi być w hello tego samego regionu Azure i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e5346-139">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="e5346-140">Warstwy standardowa maszyn wirtualnych, takie jak, D, DS, G i GS serii maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e5346-140">Standard tier VMs, such as A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="e5346-141">Szyfrowanie dysków nie jest obecnie obsługiwane w hello następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="e5346-141">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="e5346-142">Maszyny wirtualne warstwy podstawowa.</span><span class="sxs-lookup"><span data-stu-id="e5346-142">Basic tier VMs.</span></span>
* <span data-ttu-id="e5346-143">Maszyny wirtualne utworzone za pomocą hello klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="e5346-143">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="e5346-144">Aktualizowanie kluczy kryptograficznych hello na maszynie Wirtualnej platformy już zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="e5346-144">Updating hello cryptographic keys on an already encrypted VM.</span></span>
* <span data-ttu-id="e5346-145">Integracja z usługą zarządzania kluczami lokalnego.</span><span class="sxs-lookup"><span data-stu-id="e5346-145">Integration with on-prem Key Management Service.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="e5346-146">Tworzenie usługi Azure Key Vault i kluczy</span><span class="sxs-lookup"><span data-stu-id="e5346-146">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="e5346-147">Przed rozpoczęciem upewnij się, najnowszą wersję hello tego hello Azure PowerShell moduł został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="e5346-147">Before you start, make sure that hello latest version of hello Azure PowerShell module has been installed.</span></span> <span data-ttu-id="e5346-148">Aby uzyskać więcej informacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e5346-148">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="e5346-149">W przykładach poleceń hello Zamień wszystkie parametry przykład własne nazwy, lokalizacji i wartości klucza.</span><span class="sxs-lookup"><span data-stu-id="e5346-149">Throughout hello command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="e5346-150">Witaj następujących przykładach użyto Konwencji *myResourceGroup*, *myKeyVault*, *myVM*itp.</span><span class="sxs-lookup"><span data-stu-id="e5346-150">hello following examples use a convention of *myResourceGroup*, *myKeyVault*, *myVM*, etc.</span></span>

<span data-ttu-id="e5346-151">pierwszym krokiem Hello jest toocreate toostore usługi Azure Key Vault kluczy kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="e5346-151">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="e5346-152">Usługa Azure Key Vault może przechowywać klucze i klucze tajne, lub haseł, które pozwalają toosecurely wdrożyć je w aplikacji i usług.</span><span class="sxs-lookup"><span data-stu-id="e5346-152">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="e5346-153">Szyfrowanie dysków wirtualnych tworzenia toostore Key Vault klucza kryptograficznego, który jest używany tooencrypt lub odszyfrować dysków wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e5346-153">For virtual disk encryption, you create a Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span> 

<span data-ttu-id="e5346-154">Włącz hello dostawcy usługi Azure Key Vault w ramach Twojej subskrypcji platformy Azure z [AzureRmResourceProvider rejestru](/powershell/module/azurerm.resources/register-azurermresourceprovider), następnie utwórz nową grupę zasobów o [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="e5346-154">Enable hello Azure Key Vault provider within your Azure subscription with [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), then create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="e5346-155">Witaj poniższy przykład tworzy nazwę grupy zasobów *myResourceGroup* w hello *wschodnie stany USA* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="e5346-155">hello following example creates a resource group name *myResourceGroup* in hello *East US* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

<span data-ttu-id="e5346-156">Hello Azure Key Vault zawierającego hello kluczy kryptograficznych i obliczeniowe skojarzone zasoby, takie jak magazyn i hello samej maszyny Wirtualnej musi znajdować się w hello tego samego regionu.</span><span class="sxs-lookup"><span data-stu-id="e5346-156">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="e5346-157">Tworzenie usługi Azure Key Vault z [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) i Włącz hello Key Vault służących do szyfrowania dysku.</span><span class="sxs-lookup"><span data-stu-id="e5346-157">Create an Azure Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="e5346-158">Określ unikatową nazwę usługi Key Vault *keyVaultName* w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e5346-158">Specify a unique Key Vault name for *keyVaultName* as follows:</span></span>

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

<span data-ttu-id="e5346-159">Mogą być przechowywane przy użyciu oprogramowania lub sprzętu modelu zabezpieczeń (HSM) ochronę kluczy kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="e5346-159">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="e5346-160">Użycie modułów HSM wymaga premium magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="e5346-160">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="e5346-161">Brak dodatkowych kosztów toocreating premium magazynu kluczy, a nie standardowy magazyn kluczy, którego przechowuje klucze chronione przez oprogramowanie.</span><span class="sxs-lookup"><span data-stu-id="e5346-161">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="e5346-162">toocreate premium usługi Key Vault w hello poprzedzających krok dodać hello *- Sku "Premium"* parametrów.</span><span class="sxs-lookup"><span data-stu-id="e5346-162">toocreate a premium Key Vault, in hello preceding step add hello *-Sku "Premium"* parameters.</span></span> <span data-ttu-id="e5346-163">Witaj poniższym przykładzie użyto klucze chronione oprogramowaniem ponieważ utworzyliśmy standardowy magazyn kluczy.</span><span class="sxs-lookup"><span data-stu-id="e5346-163">hello following example uses software-protected keys since we created a standard Key Vault.</span></span> 

<span data-ttu-id="e5346-164">W przypadku obu modeli ochrony hello platformy Azure musi toobe udzielać dostępu do kluczy kryptograficznych hello toorequest, w przypadku, gdy hello maszyny Wirtualnej wykonuje rozruch toodecrypt hello wirtualnych dysków.</span><span class="sxs-lookup"><span data-stu-id="e5346-164">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="e5346-165">Tworzenie klucza kryptograficznego w magazyn kluczy o [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span><span class="sxs-lookup"><span data-stu-id="e5346-165">Create a cryptographic key in your Key Vault with [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span></span> <span data-ttu-id="e5346-166">Witaj poniższym przykładzie jest tworzony klucz o nazwie *klucze*:</span><span class="sxs-lookup"><span data-stu-id="e5346-166">hello following example creates a key named *myKey*:</span></span>

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-hello-azure-active-directory-service-principal"></a><span data-ttu-id="e5346-167">Utwórz hello nazwy głównej usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e5346-167">Create hello Azure Active Directory service principal</span></span>
<span data-ttu-id="e5346-168">Gdy dyski wirtualne są szyfrowane lub odszyfrować, należy określić konto toohandle hello uwierzytelniania i wymiana kluczy kryptograficznych z magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="e5346-168">When virtual disks are encrypted or decrypted, you specify an account toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="e5346-169">To konto, nazwy głównej usługi Azure Active Directory umożliwia toorequest platformy Azure hello hello odpowiednich kluczy kryptograficznych imieniu hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5346-169">This account, an Azure Active Directory service principal, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="e5346-170">Domyślne wystąpienie usługi Azure Active Directory jest dostępne w Twojej subskrypcji, chociaż w wielu organizacjach są wyposażone w dedykowane katalogów usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e5346-170">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="e5346-171">Tworzenie nazwy głównej usługi w usłudze Azure Active Directory z [AzureRmADServicePrincipal nowy](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span><span class="sxs-lookup"><span data-stu-id="e5346-171">Create a service principal in Azure Active Directory with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span></span> <span data-ttu-id="e5346-172">toospecify bezpieczne hasło, należy wykonać hello [ograniczenia w usłudze Azure Active Directory i zasadami haseł](../../active-directory/active-directory-passwords-policy.md):</span><span class="sxs-lookup"><span data-stu-id="e5346-172">toospecify a secure password, follow hello [Password policies and restrictions in Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):</span></span>

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

<span data-ttu-id="e5346-173">toosuccessfully zaszyfrować lub odszyfrować dysków wirtualnych, uprawnienia do klucza kryptograficznego hello przechowywane w magazynie klucza musi być klucze hello tooread główną usługi Azure Active Directory zestaw toopermit hello.</span><span class="sxs-lookup"><span data-stu-id="e5346-173">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory service principal tooread hello keys.</span></span> <span data-ttu-id="e5346-174">Ustaw uprawnienia na magazyn kluczy o [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span><span class="sxs-lookup"><span data-stu-id="e5346-174">Set permissions on your Key Vault with [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a><span data-ttu-id="e5346-175">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e5346-175">Create virtual machine</span></span>
<span data-ttu-id="e5346-176">tootest hello proces szyfrowania, Utwórz Maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="e5346-176">tootest hello encryption process, let's create a VM.</span></span> <span data-ttu-id="e5346-177">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM* przy użyciu *systemu Windows Server 2016 Datacenter* obrazu:</span><span class="sxs-lookup"><span data-stu-id="e5346-177">hello following example creates a VM named *myVM* using a *Windows Server 2016 Datacenter* image:</span></span>

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


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="e5346-178">Szyfrowanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e5346-178">Encrypt virtual machine</span></span>
<span data-ttu-id="e5346-179">dyski wirtualne hello tooencrypt, przełączeniem razem wszystkie poprzednie składniki hello:</span><span class="sxs-lookup"><span data-stu-id="e5346-179">tooencrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="e5346-180">Określ hello nazwy głównej usługi Azure Active Directory i hasło.</span><span class="sxs-lookup"><span data-stu-id="e5346-180">Specify hello Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="e5346-181">Określ hello Key Vault toostore hello metadanych dla zaszyfrowanych dysków.</span><span class="sxs-lookup"><span data-stu-id="e5346-181">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="e5346-182">Określ toouse kluczy kryptograficznych hello hello rzeczywiste szyfrowania i odszyfrowywania.</span><span class="sxs-lookup"><span data-stu-id="e5346-182">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="e5346-183">Określ, czy tooencrypt hello systemu operacyjnego, dysku dysków z danymi hello lub wszystkie.</span><span class="sxs-lookup"><span data-stu-id="e5346-183">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="e5346-184">Szyfrowanie maszyny Wirtualnej z [AzureRmVMDiskEncryptionExtension zestaw](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) przy użyciu klucza usługi Azure Key Vault hello i poświadczenia główne usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e5346-184">Encrypt your VM with [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) using hello Azure Key Vault key and Azure Active Directory service principal credentials.</span></span> <span data-ttu-id="e5346-185">Witaj poniższy przykład pobiera wszystkie informacje o kluczu hello, a następnie szyfruje hello maszyny Wirtualnej o nazwie *myVM*:</span><span class="sxs-lookup"><span data-stu-id="e5346-185">hello following example retrieves all hello key information then encrypts hello VM named *myVM*:</span></span>

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

<span data-ttu-id="e5346-186">Zaakceptuj hello toocontinue monitu hello szyfrowanie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5346-186">Accept hello prompt toocontinue with hello VM encryption.</span></span> <span data-ttu-id="e5346-187">podczas procesu hello uruchamia ponownie Hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5346-187">hello VM restarts during hello process.</span></span> <span data-ttu-id="e5346-188">Po zakończeniu procesu szyfrowania hello i hello maszyny Wirtualnej został ponownie uruchomiony, przejrzyj hello stanu szyfrowania z [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span><span class="sxs-lookup"><span data-stu-id="e5346-188">Once hello encryption process completes and hello VM has rebooted, review hello encryption status with [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span></span>

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

<span data-ttu-id="e5346-189">Witaj danych wyjściowych jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="e5346-189">hello output is similar toohello following example:</span></span>

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a><span data-ttu-id="e5346-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e5346-190">Next steps</span></span>
* <span data-ttu-id="e5346-191">Aby uzyskać więcej informacji na temat zarządzania usługą Azure Key Vault, zobacz [Konfigurowanie magazynu kluczy dla maszyn wirtualnych](key-vault-setup.md).</span><span class="sxs-lookup"><span data-stu-id="e5346-191">For more information about managing Azure Key Vault, see [Set up Key Vault for virtual machines](key-vault-setup.md).</span></span>
* <span data-ttu-id="e5346-192">Aby uzyskać więcej informacji o szyfrowaniu dysków, takich jak przygotowywanie zaszyfrowanego niestandardowego wirtualna tooupload tooAzure, zobacz [szyfrowania dysków Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="e5346-192">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
