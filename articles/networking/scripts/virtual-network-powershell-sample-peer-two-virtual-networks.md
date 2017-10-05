---
title: "Przykładowy skrypt programu PowerShell Azure - równorzędnej dwie sieci wirtualne | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 51c0b98727e148671cfd7ab2b31ffd1c705d8a4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="798b3-103">Dwie wirtualne sieci równorzędne</span><span class="sxs-lookup"><span data-stu-id="798b3-103">Peer two virtual networks</span></span>

<span data-ttu-id="798b3-104">Ten skrypt tworzy i łączy dwie sieci wirtualne w tej samej trhough region sieć platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="798b3-104">This script creates and connects two virtual networks in the same region trhough the Azure network.</span></span> <span data-ttu-id="798b3-105">Po uruchomieniu skryptu spowoduje utworzenie komunikacji równorzędnej między dwiema sieciami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="798b3-105">After running the script, you will create a peering between two virtual networks.</span></span>

<span data-ttu-id="798b3-106">W razie potrzeby zainstalować program Azure PowerShell przy użyciu instrukcji w [Przewodnik programu Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), a następnie uruchom `Login-AzureRmAccount` można utworzyć połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="798b3-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="798b3-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="798b3-107">Sample script</span></span>

<span data-ttu-id="798b3-108">[!code-azurepowershell[główne](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "elementu równorzędnego dwiema sieciami")]</span><span class="sxs-lookup"><span data-stu-id="798b3-108">[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Peer two networks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="798b3-109">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="798b3-109">Clean up deployment</span></span> 

<span data-ttu-id="798b3-110">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="798b3-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="798b3-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="798b3-111">Script explanation</span></span>

<span data-ttu-id="798b3-112">Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, maszyny wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="798b3-112">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="798b3-113">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="798b3-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="798b3-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="798b3-114">Command</span></span> | <span data-ttu-id="798b3-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="798b3-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="798b3-116">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="798b3-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="798b3-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="798b3-117">Creates a resource group in which all resources are stored.</span></span> | 
| [<span data-ttu-id="798b3-118">Nowy AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="798b3-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork)| <span data-ttu-id="798b3-119">Tworzy sieć wirtualna platformy Azure i podsieć.</span><span class="sxs-lookup"><span data-stu-id="798b3-119">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="798b3-120">Dodaj AzureRmVirtualNetworkPeering</span><span class="sxs-lookup"><span data-stu-id="798b3-120">Add-AzureRmVirtualNetworkPeering</span></span>](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering) | <span data-ttu-id="798b3-121">Tworzy komunikacji równorzędnej między dwiema sieciami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="798b3-121">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="798b3-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="798b3-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="798b3-123">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="798b3-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="798b3-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="798b3-124">Next steps</span></span>

<span data-ttu-id="798b3-125">Aby uzyskać więcej informacji dotyczących programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="798b3-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="798b3-126">Dodatkowe przykłady skryptów PowerShell sieci można znaleźć w [Azure Przegląd dokumentacji](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="798b3-126">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>