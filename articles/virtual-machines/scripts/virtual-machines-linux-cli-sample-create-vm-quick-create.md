---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Szybkie tworzenie maszyny Wirtualnej systemu Linux | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt Azure CLI — szybkie tworzenie maszyny Wirtualnej systemu Linux"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: edecf274f4e401af3603e5be37a989e2e0eb22c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine"></a><span data-ttu-id="371c1-103">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="371c1-103">Create a virtual machine</span></span>

<span data-ttu-id="371c1-104">Ten skrypt tworzy maszynę wirtualną platformy Azure z systemem operacyjnym Ubuntu i powiązanych zasobów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="371c1-104">This script creates an Azure Virtual Machine with an Ubuntu operating system and related networking resources.</span></span> <span data-ttu-id="371c1-105">Po uruchomieniu skryptu hello, można uzyskać dostępu do maszyny wirtualnej hello za pomocą protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="371c1-105">After running hello script, you can access hello virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="371c1-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="371c1-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-vm-quick.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="371c1-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="371c1-107">Clean up deployment</span></span> 

<span data-ttu-id="371c1-108">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="371c1-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="371c1-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="371c1-109">Script explanation</span></span>

<span data-ttu-id="371c1-110">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów maszyny wirtualnej, a wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="371c1-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="371c1-111">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="371c1-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="371c1-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="371c1-112">Command</span></span> | <span data-ttu-id="371c1-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="371c1-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="371c1-114">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="371c1-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="371c1-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="371c1-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="371c1-116">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="371c1-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="371c1-117">Tworzy maszynę wirtualną hello i łączy go toohello karty sieciowej, sieć wirtualną, podsieci i grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="371c1-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="371c1-118">To polecenie określa również toobe obrazu maszyny wirtualnej hello używane i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="371c1-118">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="371c1-119">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="371c1-119">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="371c1-120">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="371c1-120">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="371c1-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="371c1-121">Next steps</span></span>

<span data-ttu-id="371c1-122">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="371c1-122">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="371c1-123">Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="371c1-123">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
