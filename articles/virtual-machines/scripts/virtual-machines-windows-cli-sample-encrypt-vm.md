---
title: "Azure CLI skrypt przykładowy — zaszyfrować maszyny Wirtualnej systemu Windows | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 9574d779982c939aa970cd4bdf7df6e66793e3b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="encrypt-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="f26df-103">Szyfrowanie maszyny wirtualnej systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f26df-103">Encrypt a Windows virtual machine in Azure</span></span>

<span data-ttu-id="f26df-104">Ten skrypt tworzy bezpieczne usługi Azure Key Vault, klucze szyfrowania, nazwy głównej usługi Azure Active Directory i maszyny wirtualnej systemu Windows (VM).</span><span class="sxs-lookup"><span data-stu-id="f26df-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Windows virtual machine (VM).</span></span> <span data-ttu-id="f26df-105">Maszyna wirtualna jest następnie szyfrowany przy użyciu klucza szyfrowania z magazynu kluczy i poświadczenia główne usługi.</span><span class="sxs-lookup"><span data-stu-id="f26df-105">The VM is then encrypted using the encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f26df-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="f26df-106">Sample script</span></span>

<span data-ttu-id="f26df-107">[!code-azurecli-interactive[główne](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_windows_vm.sh "dysków szyfrowania maszyny Wirtualnej")]</span><span class="sxs-lookup"><span data-stu-id="f26df-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_windows_vm.sh "Encrypt VM disks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="f26df-108">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="f26df-108">Clean up deployment</span></span> 

<span data-ttu-id="f26df-109">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="f26df-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f26df-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="f26df-110">Script explanation</span></span>

<span data-ttu-id="f26df-111">Ten skrypt używa następujących poleceń w celu utworzenia grupy zasobów, usługi Azure Key Vault nazwy głównej usługi, maszyny wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="f26df-111">This script uses the following commands to create a resource group, Azure Key Vault, service principal, virtual machine, and all related resources.</span></span> <span data-ttu-id="f26df-112">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="f26df-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f26df-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="f26df-113">Command</span></span> | <span data-ttu-id="f26df-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="f26df-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f26df-115">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="f26df-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f26df-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="f26df-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f26df-117">Utwórz az keyvault</span><span class="sxs-lookup"><span data-stu-id="f26df-117">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="f26df-118">Tworzy magazynu kluczy Azure do przechowywania zabezpieczonych danych, takie jak klucze szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="f26df-118">Creates an Azure Key Vault to store secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="f26df-119">Utwórz klucz keyvault az</span><span class="sxs-lookup"><span data-stu-id="f26df-119">az keyvault key create</span></span>](https://docs.microsoft.com/cli/azure/keyvault/key#create) | <span data-ttu-id="f26df-120">Tworzy klucz szyfrowania magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="f26df-120">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="f26df-121">ad az sp utworzyć do rbac</span><span class="sxs-lookup"><span data-stu-id="f26df-121">az ad sp create-for-rbac</span></span>](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | <span data-ttu-id="f26df-122">Tworzy nazwę główną usługi do bezpiecznego uwierzytelniania i kontroli dostępu do kluczy szyfrowania usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f26df-122">Creates an Azure Active Directory service principal to securely authenticate and control access to encryption keys.</span></span> |
| [<span data-ttu-id="f26df-123">keyvault az set-policy.</span><span class="sxs-lookup"><span data-stu-id="f26df-123">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="f26df-124">Ustawia uprawnienia Key Vault w celu udzielenia dostępu główną usługi do kluczy szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="f26df-124">Sets permissions on the Key Vault to grant the service principal access to encryption keys.</span></span> |
| [<span data-ttu-id="f26df-125">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="f26df-125">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="f26df-126">Tworzy maszynę wirtualną i podłączony do karty sieciowej, sieci wirtualnej, podsieci i NSG.</span><span class="sxs-lookup"><span data-stu-id="f26df-126">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="f26df-127">To polecenie określa również obraz maszyny wirtualnej ma być używany, a poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="f26df-127">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="f26df-128">Włącz szyfrowanie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="f26df-128">az vm encryption enable</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | <span data-ttu-id="f26df-129">Włącza szyfrowanie na maszynie Wirtualnej przy użyciu poświadczeń głównej usługi i klucza szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="f26df-129">Enables encryption on a VM using the service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="f26df-130">Pokaż szyfrowania maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="f26df-130">az vm encryption show</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#show) | <span data-ttu-id="f26df-131">Wyświetla stan procesu szyfrowania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f26df-131">Shows the status of the VM encryption process.</span></span> |
| [<span data-ttu-id="f26df-132">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="f26df-132">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="f26df-133">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="f26df-133">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f26df-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f26df-134">Next steps</span></span>

<span data-ttu-id="f26df-135">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f26df-135">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f26df-136">Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w [dokumentacji maszyny Wirtualnej systemu Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%windows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f26df-136">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%windows%2ftoc.json).</span></span>
