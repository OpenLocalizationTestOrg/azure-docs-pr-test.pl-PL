---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia - zaszyfrować Maszynę wirtualną z systemem Windows | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — zaszyfrować maszyny Wirtualnej systemu Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 7a9928467f818cd5358d3d19bff5129d8fa21313
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="9341e-103">Szyfrowanie maszyny wirtualnej systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="9341e-103">Encrypt a Windows virtual machine in Azure</span></span>

<span data-ttu-id="9341e-104">Ten skrypt tworzy bezpieczne usługi Azure Key Vault, klucze szyfrowania, nazwy głównej usługi Azure Active Directory i maszyny wirtualnej systemu Windows (VM).</span><span class="sxs-lookup"><span data-stu-id="9341e-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Windows virtual machine (VM).</span></span> <span data-ttu-id="9341e-105">Hello maszyny Wirtualnej jest następnie szyfrowany przy użyciu klucza szyfrowania hello z magazynu kluczy i poświadczenia główne.</span><span class="sxs-lookup"><span data-stu-id="9341e-105">hello VM is then encrypted using hello encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9341e-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="9341e-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_windows_vm.sh "Encrypt VM disks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9341e-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="9341e-107">Clean up deployment</span></span> 

<span data-ttu-id="9341e-108">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="9341e-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="9341e-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="9341e-109">Script explanation</span></span>

<span data-ttu-id="9341e-110">Ten skrypt używa hello następujące polecenia toocreate zasobów grupy usługi Azure Key Vault usługi głównej, maszyny wirtualnej, i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="9341e-110">This script uses hello following commands toocreate a resource group, Azure Key Vault, service principal, virtual machine, and all related resources.</span></span> <span data-ttu-id="9341e-111">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="9341e-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9341e-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="9341e-112">Command</span></span> | <span data-ttu-id="9341e-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="9341e-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9341e-114">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="9341e-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9341e-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="9341e-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9341e-116">Utwórz az keyvault</span><span class="sxs-lookup"><span data-stu-id="9341e-116">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="9341e-117">Tworzy usługi Azure Key Vault toostore bezpiecznego dane, takie jak klucze szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="9341e-117">Creates an Azure Key Vault toostore secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="9341e-118">Utwórz klucz keyvault az</span><span class="sxs-lookup"><span data-stu-id="9341e-118">az keyvault key create</span></span>](https://docs.microsoft.com/cli/azure/keyvault/key#create) | <span data-ttu-id="9341e-119">Tworzy klucz szyfrowania magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="9341e-119">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="9341e-120">ad az sp utworzyć do rbac</span><span class="sxs-lookup"><span data-stu-id="9341e-120">az ad sp create-for-rbac</span></span>](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | <span data-ttu-id="9341e-121">Tworzy usługę Azure Active Directory główna toosecurely uwierzytelniania i kontroli dostępu tooencryption kluczy.</span><span class="sxs-lookup"><span data-stu-id="9341e-121">Creates an Azure Active Directory service principal toosecurely authenticate and control access tooencryption keys.</span></span> |
| [<span data-ttu-id="9341e-122">keyvault az set-policy.</span><span class="sxs-lookup"><span data-stu-id="9341e-122">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="9341e-123">Ustawia uprawnienia na powitania Key Vault toogrant hello usługi głównej dostępu tooencryption kluczy.</span><span class="sxs-lookup"><span data-stu-id="9341e-123">Sets permissions on hello Key Vault toogrant hello service principal access tooencryption keys.</span></span> |
| [<span data-ttu-id="9341e-124">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="9341e-124">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="9341e-125">Tworzy maszynę wirtualną hello i łączy go toohello karty sieciowej, sieć wirtualną, podsieci i NSG.</span><span class="sxs-lookup"><span data-stu-id="9341e-125">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="9341e-126">To polecenie określa również toobe obrazu maszyny wirtualnej hello używane i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="9341e-126">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="9341e-127">Włącz szyfrowanie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="9341e-127">az vm encryption enable</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | <span data-ttu-id="9341e-128">Włącza szyfrowanie na maszynie Wirtualnej za pomocą poświadczenia główne hello usługi i klucza szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="9341e-128">Enables encryption on a VM using hello service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="9341e-129">Pokaż szyfrowania maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="9341e-129">az vm encryption show</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#show) | <span data-ttu-id="9341e-130">Wyświetla stan hello hello proces szyfrowania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9341e-130">Shows hello status of hello VM encryption process.</span></span> |
| [<span data-ttu-id="9341e-131">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="9341e-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="9341e-132">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="9341e-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9341e-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9341e-133">Next steps</span></span>

<span data-ttu-id="9341e-134">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9341e-134">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9341e-135">Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%windows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9341e-135">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%windows%2ftoc.json).</span></span>
