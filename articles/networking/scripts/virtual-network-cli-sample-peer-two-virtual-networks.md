---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia - Peer dwie sieci wirtualne | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 54dabb2b9e05951d10f1b6b4f61ca592ce11d364
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="08244-103">Dwie wirtualne sieci równorzędne</span><span class="sxs-lookup"><span data-stu-id="08244-103">Peer two virtual networks</span></span>

<span data-ttu-id="08244-104">Ten skrypt tworzy i łączy dwie sieci wirtualne w hello tego samego regionu hello trhough sieć platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="08244-104">This script creates and connects two virtual networks in hello same region trhough hello Azure network.</span></span> <span data-ttu-id="08244-105">Po uruchomieniu skryptu hello, zostanie utworzona komunikacji równorzędnej między dwiema sieciami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="08244-105">After running hello script, you will create a peering between two virtual networks.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="08244-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="08244-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "Peer two networks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="08244-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="08244-107">Clean up deployment</span></span> 

<span data-ttu-id="08244-108">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="08244-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="08244-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="08244-109">Script explanation</span></span>

<span data-ttu-id="08244-110">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów maszyny wirtualnej, a wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="08244-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="08244-111">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="08244-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="08244-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="08244-112">Command</span></span> | <span data-ttu-id="08244-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="08244-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="08244-114">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="08244-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="08244-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="08244-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="08244-116">Tworzenie sieci wirtualnej sieci az</span><span class="sxs-lookup"><span data-stu-id="08244-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="08244-117">Tworzy sieć wirtualna platformy Azure i podsieć.</span><span class="sxs-lookup"><span data-stu-id="08244-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="08244-118">równorzędna az sieci wirtualne sieci równorzędne — tworzenie</span><span class="sxs-lookup"><span data-stu-id="08244-118">az network vnet peering create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/peering#create) | <span data-ttu-id="08244-119">Tworzy komunikacji równorzędnej między dwiema sieciami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="08244-119">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="08244-120">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="08244-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="08244-121">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="08244-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="08244-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="08244-122">Next steps</span></span>

<span data-ttu-id="08244-123">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="08244-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="08244-124">Dodatkowe przykłady skryptów sieci interfejsu wiersza polecenia można znaleźć w hello [Azure Przegląd dokumentacji](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="08244-124">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md).</span></span>
