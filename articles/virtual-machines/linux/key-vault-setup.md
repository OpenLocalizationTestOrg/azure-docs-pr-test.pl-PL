---
title: "Konfigurowanie usługi Azure Key Vault dla maszyn wirtualnych systemu Linux | Dokumentacja firmy Microsoft"
description: "Jak skonfigurować magazyn kluczy do użycia z maszyny wirtualnej platformy Azure Resource Manager 2.0 interfejsu wiersza polecenia."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: 2cc9b4c978e9a4deb0c8443c4b0f9e301a7cf492
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-up-key-vault-for-virtual-machines-with-the-azure-cli-20"></a><span data-ttu-id="23931-103">Jak skonfigurować magazyn kluczy dla maszyn wirtualnych z 2.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="23931-103">How to set up Key Vault for virtual machines with the Azure CLI 2.0</span></span>

<span data-ttu-id="23931-104">W stosie usługi Azure Resource Manager kluczy tajnych/certyfikaty są modelowane jako zasoby, które są udostępniane przez usługi Key Vault.</span><span class="sxs-lookup"><span data-stu-id="23931-104">In the Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by Key Vault.</span></span> <span data-ttu-id="23931-105">Aby dowiedzieć się więcej na temat usługi Azure Key Vault, zobacz [co to jest usługa Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="23931-105">To learn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="23931-106">W kolejności dla usługi Key Vault ma być używany z maszyn wirtualnych Menedżera zasobów Azure *EnabledForDeployment* właściwość na magazynu kluczy musi być ustawiona na wartość true.</span><span class="sxs-lookup"><span data-stu-id="23931-106">In order for Key Vault to be used with Azure Resource Manager VMs, the *EnabledForDeployment* property on Key Vault must be set to true.</span></span> <span data-ttu-id="23931-107">W tym artykule przedstawiono sposób konfigurowania usługi Key Vault do użycia z programem Azure maszynach wirtualnych (VM) używa interfejsu wiersza polecenia Azure w wersji 2.0.</span><span class="sxs-lookup"><span data-stu-id="23931-107">This article shows you how to set up Key Vault for use with Azure virtual machines (VMs) using the Azure CLI 2.0.</span></span> <span data-ttu-id="23931-108">Czynności te można również wykonać przy użyciu [interfejsu wiersza polecenia platformy Azure w wersji 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="23931-108">You can also perform these steps with the [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="23931-109">Aby wykonać te kroki, należy najnowszej [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zalogowany do konta platformy Azure przy użyciu [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="23931-109">To perform these steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="23931-110">Tworzenie magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="23931-110">Create a Key Vault</span></span>
<span data-ttu-id="23931-111">Tworzenie magazynu kluczy i przypisać zasady wdrażania z [az keyvault utworzyć](/cli/azure/keyvault#create).</span><span class="sxs-lookup"><span data-stu-id="23931-111">Create a key vault and assign the deployment policy with [az keyvault create](/cli/azure/keyvault#create).</span></span> <span data-ttu-id="23931-112">Poniższy przykład tworzy magazyn kluczy o nazwie `myKeyVault` w `myResourceGroup` grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="23931-112">The following example creates a key vault named `myKeyVault` in the `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a><span data-ttu-id="23931-113">Zaktualizuj magazyn kluczy do użytku z maszynami wirtualnymi</span><span class="sxs-lookup"><span data-stu-id="23931-113">Update a Key Vault for use with VMs</span></span>
<span data-ttu-id="23931-114">Ustaw zasady wdrażania na istniejącego klucza magazynu z [az keyvault aktualizacji](/cli/azure/keyvault#update).</span><span class="sxs-lookup"><span data-stu-id="23931-114">Set the deployment policy on an existing key vault with [az keyvault update](/cli/azure/keyvault#update).</span></span> <span data-ttu-id="23931-115">Następujące aktualizacje magazyn kluczy o nazwie `myKeyVault` w `myResourceGroup` grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="23931-115">The following updates the key vault named `myKeyVault` in the `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-to-set-up-key-vault"></a><span data-ttu-id="23931-116">Konfigurowanie usługi Key Vault za pomocą szablonów</span><span class="sxs-lookup"><span data-stu-id="23931-116">Use templates to set up Key Vault</span></span>
<span data-ttu-id="23931-117">Gdy używasz szablonu, musisz ustawić `enabledForDeployment` właściwości `true` klucza magazynu zasobów w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="23931-117">When you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource as follows:</span></span>

```json
{
    "type": "Microsoft.KeyVault/vaults",
    "name": "ContosoKeyVault",
    "apiVersion": "2015-06-01",
    "location": "<location-of-key-vault>",
    "properties": {
    "enabledForDeployment": "true",
    ....
    ....
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="23931-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="23931-118">Next steps</span></span>
<span data-ttu-id="23931-119">Inne opcje, które można skonfigurować podczas tworzenia usługi Key Vault przy użyciu szablonów, zobacz [utworzyć magazyn kluczy](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="23931-119">For other options that you can configure when you create a Key Vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
