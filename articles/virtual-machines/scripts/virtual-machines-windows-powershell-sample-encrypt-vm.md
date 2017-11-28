---
title: "Przykładowy skrypt programu PowerShell - aaaAzure zaszyfrować Maszynę wirtualną z systemem Windows | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — zaszyfrować maszyny Wirtualnej systemu Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 80c52a0b734a52a051ed30026b294840fd521143
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="e82a0-103">Szyfrowanie maszyny wirtualnej systemu Windows, przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e82a0-103">Encrypt a Windows virtual machine with Azure PowerShell</span></span>

<span data-ttu-id="e82a0-104">Ten skrypt tworzy bezpieczne usługi Azure Key Vault, klucze szyfrowania, nazwy głównej usługi Azure Active Directory i maszyny wirtualnej systemu Windows (VM).</span><span class="sxs-lookup"><span data-stu-id="e82a0-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Windows virtual machine (VM).</span></span> <span data-ttu-id="e82a0-105">Hello maszyny Wirtualnej jest następnie szyfrowany przy użyciu klucza szyfrowania hello z magazynu kluczy i poświadczenia główne.</span><span class="sxs-lookup"><span data-stu-id="e82a0-105">hello VM is then encrypted using hello encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e82a0-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="e82a0-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "Encrypt VM disks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e82a0-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="e82a0-107">Clean up deployment</span></span> 

<span data-ttu-id="e82a0-108">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="e82a0-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="e82a0-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="e82a0-109">Script explanation</span></span>

<span data-ttu-id="e82a0-110">Ten skrypt używa hello następujące polecenia toocreate hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="e82a0-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="e82a0-111">Każdy element w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="e82a0-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e82a0-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="e82a0-112">Command</span></span> | <span data-ttu-id="e82a0-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="e82a0-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e82a0-114">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e82a0-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="e82a0-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="e82a0-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e82a0-116">Nowy AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="e82a0-116">New-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/new-azurermkeyvault) | <span data-ttu-id="e82a0-117">Tworzy usługi Azure Key Vault toostore bezpiecznego dane, takie jak klucze szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="e82a0-117">Creates an Azure Key Vault toostore secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="e82a0-118">Dodaj AzureKeyVaultKey</span><span class="sxs-lookup"><span data-stu-id="e82a0-118">Add-AzureKeyVaultKey</span></span>](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) | <span data-ttu-id="e82a0-119">Tworzy klucz szyfrowania magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="e82a0-119">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="e82a0-120">Nowe AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="e82a0-120">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="e82a0-121">Tworzy usługę Azure Active Directory główna toosecurely uwierzytelniania i kontroli dostępu tooencryption kluczy.</span><span class="sxs-lookup"><span data-stu-id="e82a0-121">Creates an Azure Active Directory service principal toosecurely authenticate and control access tooencryption keys.</span></span> |
| [<span data-ttu-id="e82a0-122">Set-AzureRmKeyVaultAccessPolicy</span><span class="sxs-lookup"><span data-stu-id="e82a0-122">Set-AzureRmKeyVaultAccessPolicy</span></span>](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) | <span data-ttu-id="e82a0-123">Ustawia uprawnienia na powitania Key Vault toogrant hello usługi głównej dostępu tooencryption kluczy.</span><span class="sxs-lookup"><span data-stu-id="e82a0-123">Sets permissions on hello Key Vault toogrant hello service principal access tooencryption keys.</span></span> |
| [<span data-ttu-id="e82a0-124">Nowe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="e82a0-124">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="e82a0-125">Tworzy konfiguracji podsieci.</span><span class="sxs-lookup"><span data-stu-id="e82a0-125">Creates a subnet configuration.</span></span> <span data-ttu-id="e82a0-126">Ta konfiguracja jest używana z procesu tworzenia hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e82a0-126">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="e82a0-127">Nowy AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="e82a0-127">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="e82a0-128">Tworzy sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="e82a0-128">Creates a virtual network.</span></span> |
| [<span data-ttu-id="e82a0-129">Nowe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="e82a0-129">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="e82a0-130">Tworzy publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="e82a0-130">Creates a public IP address.</span></span> |
| [<span data-ttu-id="e82a0-131">Nowe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="e82a0-131">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="e82a0-132">Tworzy konfiguracji reguły grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="e82a0-132">Creates a network security group rule configuration.</span></span> <span data-ttu-id="e82a0-133">Ta konfiguracja jest używane toocreate reguły NSG, po utworzeniu hello NSG.</span><span class="sxs-lookup"><span data-stu-id="e82a0-133">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="e82a0-134">Nowe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="e82a0-134">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="e82a0-135">Tworzy sieciową grupę zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e82a0-135">Creates a network security group.</span></span> |
| [<span data-ttu-id="e82a0-136">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="e82a0-136">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="e82a0-137">Pobiera informacje o podsieci.</span><span class="sxs-lookup"><span data-stu-id="e82a0-137">Gets subnet information.</span></span> <span data-ttu-id="e82a0-138">Te informacje jest używany podczas tworzenia interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="e82a0-138">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="e82a0-139">Nowe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="e82a0-139">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="e82a0-140">Tworzy interfejs sieciowy.</span><span class="sxs-lookup"><span data-stu-id="e82a0-140">Creates a network interface.</span></span> |
| [<span data-ttu-id="e82a0-141">Nowe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="e82a0-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="e82a0-142">Tworzy konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e82a0-142">Creates a VM configuration.</span></span> <span data-ttu-id="e82a0-143">Ta konfiguracja zawiera informacje, takie jak nazwa maszyny Wirtualnej, system operacyjny i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="e82a0-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="e82a0-144">Konfiguracja Hello jest używany podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e82a0-144">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="e82a0-145">Nowe AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="e82a0-145">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="e82a0-146">Utwórz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="e82a0-146">Create a virtual machine.</span></span> |
| [<span data-ttu-id="e82a0-147">Get-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="e82a0-147">Get-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/get-azurermkeyvault) | <span data-ttu-id="e82a0-148">Pobiera wymagane informacje na powitania magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="e82a0-148">Gets required information on hello Key Vault</span></span> |
| [<span data-ttu-id="e82a0-149">Zestaw AzureRmVMDiskEncryptionExtension</span><span class="sxs-lookup"><span data-stu-id="e82a0-149">Set-AzureRmVMDiskEncryptionExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) | <span data-ttu-id="e82a0-150">Włącza szyfrowanie na maszynie Wirtualnej za pomocą poświadczenia główne hello usługi i klucza szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="e82a0-150">Enables encryption on a VM using hello service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="e82a0-151">Get-AzureRmVmDiskEncryptionStatus</span><span class="sxs-lookup"><span data-stu-id="e82a0-151">Get-AzureRmVmDiskEncryptionStatus</span></span>](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) | <span data-ttu-id="e82a0-152">Wyświetla stan hello hello proces szyfrowania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e82a0-152">Shows hello status of hello VM encryption process.</span></span> |
| [<span data-ttu-id="e82a0-153">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e82a0-153">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="e82a0-154">Usuwa grupę zasobów i wszystkie zasoby zawarte w ciągu.</span><span class="sxs-lookup"><span data-stu-id="e82a0-154">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e82a0-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e82a0-155">Next steps</span></span>

<span data-ttu-id="e82a0-156">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e82a0-156">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e82a0-157">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e82a0-157">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
