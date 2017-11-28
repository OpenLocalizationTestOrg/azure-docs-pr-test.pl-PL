---
title: "Azure CLI przykładowym skrypcie - równorzędnej dwie sieci wirtualne | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie - równorzędnej dwie sieci wirtualne"
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: a2b8fda288072e2fb0087988bbd68d3e4d9031d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="9d2c0-103">Dwie wirtualne sieci równorzędne</span><span class="sxs-lookup"><span data-stu-id="9d2c0-103">Peer two virtual networks</span></span>

<span data-ttu-id="9d2c0-104">Ten skrypt tworzy i łączy dwie sieci wirtualne w tej samej trhough region sieć platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9d2c0-104">This script creates and connects two virtual networks in the same region trhough the Azure network.</span></span> <span data-ttu-id="9d2c0-105">Po uruchomieniu skryptu spowoduje utworzenie komunikacji równorzędnej między dwiema sieciami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="9d2c0-105">After running the script, you will create a peering between two virtual networks.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="9d2c0-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="9d2c0-106">Sample script</span></span>

<span data-ttu-id="9d2c0-107">[!code-azurecli-interactive[główne](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "elementu równorzędnego dwiema sieciami")]</span><span class="sxs-lookup"><span data-stu-id="9d2c0-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "Peer two networks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="9d2c0-108">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="9d2c0-108">Clean up deployment</span></span> 

<span data-ttu-id="9d2c0-109">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="9d2c0-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="9d2c0-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="9d2c0-110">Script explanation</span></span>

<span data-ttu-id="9d2c0-111">Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, maszyny wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="9d2c0-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="9d2c0-112">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="9d2c0-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9d2c0-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="9d2c0-113">Command</span></span> | <span data-ttu-id="9d2c0-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="9d2c0-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9d2c0-115">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="9d2c0-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9d2c0-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="9d2c0-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9d2c0-117">Tworzenie sieci wirtualnej sieci az</span><span class="sxs-lookup"><span data-stu-id="9d2c0-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="9d2c0-118">Tworzy sieć wirtualna platformy Azure i podsieć.</span><span class="sxs-lookup"><span data-stu-id="9d2c0-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="9d2c0-119">równorzędna az sieci wirtualne sieci równorzędne — tworzenie</span><span class="sxs-lookup"><span data-stu-id="9d2c0-119">az network vnet peering create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/peering#create) | <span data-ttu-id="9d2c0-120">Tworzy komunikacji równorzędnej między dwiema sieciami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="9d2c0-120">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="9d2c0-121">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="9d2c0-121">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="9d2c0-122">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="9d2c0-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9d2c0-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9d2c0-123">Next steps</span></span>

<span data-ttu-id="9d2c0-124">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9d2c0-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9d2c0-125">Dodatkowe przykłady skryptów sieci interfejsu wiersza polecenia można znaleźć w [Azure Przegląd dokumentacji](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9d2c0-125">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md).</span></span>
