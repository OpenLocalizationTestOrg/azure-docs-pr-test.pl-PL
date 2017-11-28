---
title: "dwie wirtualne sieci równorzędne aaaAzure przykładowy skrypt programu PowerShell — | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure - równorzędnej dwie sieci wirtualne"
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 8b66085c35de2fc30bcef57a00d7d370911d1f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="050fb-103">Dwie wirtualne sieci równorzędne</span><span class="sxs-lookup"><span data-stu-id="050fb-103">Peer two virtual networks</span></span>

<span data-ttu-id="050fb-104">Ten skrypt tworzy i łączy dwie sieci wirtualne w hello tego samego regionu hello trhough sieć platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="050fb-104">This script creates and connects two virtual networks in hello same region trhough hello Azure network.</span></span> <span data-ttu-id="050fb-105">Po uruchomieniu skryptu hello, zostanie utworzona komunikacji równorzędnej między dwiema sieciami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="050fb-105">After running hello script, you will create a peering between two virtual networks.</span></span>

<span data-ttu-id="050fb-106">W razie potrzeby zainstaluj hello Azure PowerShell przy użyciu instrukcji hello znalezione w hello [Przewodnik programu Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), a następnie uruchom `Login-AzureRmAccount` toocreate połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="050fb-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="050fb-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="050fb-107">Sample script</span></span>

[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Peer two networks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="050fb-108">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="050fb-108">Clean up deployment</span></span> 

<span data-ttu-id="050fb-109">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="050fb-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="050fb-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="050fb-110">Script explanation</span></span>

<span data-ttu-id="050fb-111">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów maszyny wirtualnej, a wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="050fb-111">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="050fb-112">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="050fb-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="050fb-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="050fb-113">Command</span></span> | <span data-ttu-id="050fb-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="050fb-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="050fb-115">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="050fb-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="050fb-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="050fb-116">Creates a resource group in which all resources are stored.</span></span> | 
| [<span data-ttu-id="050fb-117">Nowy AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="050fb-117">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork)| <span data-ttu-id="050fb-118">Tworzy sieć wirtualna platformy Azure i podsieć.</span><span class="sxs-lookup"><span data-stu-id="050fb-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="050fb-119">Dodaj AzureRmVirtualNetworkPeering</span><span class="sxs-lookup"><span data-stu-id="050fb-119">Add-AzureRmVirtualNetworkPeering</span></span>](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering) | <span data-ttu-id="050fb-120">Tworzy komunikacji równorzędnej między dwiema sieciami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="050fb-120">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="050fb-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="050fb-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="050fb-122">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="050fb-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="050fb-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="050fb-123">Next steps</span></span>

<span data-ttu-id="050fb-124">Aby uzyskać więcej informacji na powitania programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="050fb-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="050fb-125">Dodatkowe przykłady skryptów PowerShell sieci można znaleźć w hello [Azure Przegląd dokumentacji](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="050fb-125">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
