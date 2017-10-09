---
title: aaaSet zapasowej Azure Key Vault dla maszyn wirtualnych systemu Linux | Dokumentacja firmy Microsoft
description: "Jak tooset się Key Vault do użycia z maszyny wirtualnej platformy Azure Resource Manager z hello 2.0 interfejsu wiersza polecenia."
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
ms.openlocfilehash: a5dc1fbe59a71b4456ba5b9bbacdb90440064757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-key-vault-for-virtual-machines-with-hello-azure-cli-20"></a><span data-ttu-id="5883e-103">Jak tooset się Key Vault dla maszyn wirtualnych z hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5883e-103">How tooset up Key Vault for virtual machines with hello Azure CLI 2.0</span></span>

<span data-ttu-id="5883e-104">W stosie usługi Azure Resource Manager hello kluczy tajnych/certyfikaty są modelowane jako zasoby, które są udostępniane przez usługi Key Vault.</span><span class="sxs-lookup"><span data-stu-id="5883e-104">In hello Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by Key Vault.</span></span> <span data-ttu-id="5883e-105">toolearn więcej informacji na temat usługi Azure Key Vault, zobacz [co to jest usługa Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="5883e-105">toolearn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="5883e-106">Aby używać z maszynami wirtualnymi Azure Resource Manager toobe Key Vault, hello *EnabledForDeployment* tootrue musi być ustawiona właściwość na magazyn kluczy.</span><span class="sxs-lookup"><span data-stu-id="5883e-106">In order for Key Vault toobe used with Azure Resource Manager VMs, hello *EnabledForDeployment* property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="5883e-107">W tym artykule opisano sposób tooset zapasowej Key Vault do użycia z programem Azure maszynach wirtualnych (VM) przy użyciu hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="5883e-107">This article shows you how tooset up Key Vault for use with Azure virtual machines (VMs) using hello Azure CLI 2.0.</span></span> <span data-ttu-id="5883e-108">Można również wykonać te kroki hello [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5883e-108">You can also perform these steps with hello [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="5883e-109">tooperform tych kroków, należy hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="5883e-109">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="5883e-110">Tworzenie magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="5883e-110">Create a Key Vault</span></span>
<span data-ttu-id="5883e-111">Utwórz magazyn kluczy i przypisz hello zasady wdrażania z [az keyvault utworzyć](/cli/azure/keyvault#create).</span><span class="sxs-lookup"><span data-stu-id="5883e-111">Create a key vault and assign hello deployment policy with [az keyvault create](/cli/azure/keyvault#create).</span></span> <span data-ttu-id="5883e-112">Witaj poniższy przykład tworzy magazyn kluczy o nazwie `myKeyVault` w hello `myResourceGroup` grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="5883e-112">hello following example creates a key vault named `myKeyVault` in hello `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a><span data-ttu-id="5883e-113">Zaktualizuj magazyn kluczy do użytku z maszynami wirtualnymi</span><span class="sxs-lookup"><span data-stu-id="5883e-113">Update a Key Vault for use with VMs</span></span>
<span data-ttu-id="5883e-114">Ustaw zasady wdrażania hello na istniejący magazyn kluczy o [az keyvault aktualizacji](/cli/azure/keyvault#update).</span><span class="sxs-lookup"><span data-stu-id="5883e-114">Set hello deployment policy on an existing key vault with [az keyvault update](/cli/azure/keyvault#update).</span></span> <span data-ttu-id="5883e-115">Witaj następujące aktualizacje hello magazyn kluczy o nazwie `myKeyVault` w hello `myResourceGroup` grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="5883e-115">hello following updates hello key vault named `myKeyVault` in hello `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="5883e-116">Użycie szablonów tooset zapasowej magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="5883e-116">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="5883e-117">W przypadku użycia szablonu należy tooset hello `enabledForDeployment` właściwości zbyt`true` dla zasobu usługi Key Vault hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="5883e-117">When you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource as follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5883e-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5883e-118">Next steps</span></span>
<span data-ttu-id="5883e-119">Inne opcje, które można skonfigurować podczas tworzenia usługi Key Vault przy użyciu szablonów, zobacz [utworzyć magazyn kluczy](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="5883e-119">For other options that you can configure when you create a Key Vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
