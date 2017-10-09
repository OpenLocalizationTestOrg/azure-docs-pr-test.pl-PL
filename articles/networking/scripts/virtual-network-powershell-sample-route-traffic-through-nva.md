---
title: "Przykładowy skrypt programu PowerShell aaaAzure — ruch sieciowy przez urządzenie wirtualne sieci | Dokumentacja firmy Microsoft"
description: "Przykład skryptu usługi Azure PowerShell — ruch trasy przez urządzenie wirtualne zapory w sieci."
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
ms.openlocfilehash: 3b999f3289d654c00d5becb973e2883896457d52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="c9623-103">Kierować ruchem przez urządzenie wirtualne sieci</span><span class="sxs-lookup"><span data-stu-id="c9623-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="c9623-104">Ten przykładowy skrypt tworzy sieć wirtualną z podsieci frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="c9623-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="c9623-105">Tworzy również Maszynę wirtualną z tooroute włączone ruchu między dwiema podsieciami hello przekazywania pakietów IP.</span><span class="sxs-lookup"><span data-stu-id="c9623-105">It also creates a VM with IP forwarding enabled tooroute traffic between hello two subnets.</span></span> <span data-ttu-id="c9623-106">Po uruchomieniu skryptu hello można wdrażać oprogramowanie sieci, takie jak aplikacja zapory, toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c9623-106">After running hello script you can deploy network software, such as a firewall application, toohello VM.</span></span>

<span data-ttu-id="c9623-107">W razie potrzeby zainstaluj hello Azure PowerShell przy użyciu instrukcji hello znalezione w hello [Przewodnik programu Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), a następnie uruchom `Login-AzureRmAccount` toocreate połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="c9623-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c9623-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="c9623-108">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c9623-109">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="c9623-109">Clean up deployment</span></span> 

<span data-ttu-id="c9623-110">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="c9623-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a><span data-ttu-id="c9623-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="c9623-111">Script explanation</span></span>

<span data-ttu-id="c9623-112">Ten skrypt używa powitania po toocreate poleceń, grupy zasobów, sieci wirtualnej i grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="c9623-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="c9623-113">Każde polecenie w dokumentacji konkretnego toocommand łącza tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="c9623-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="c9623-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="c9623-114">Command</span></span> | <span data-ttu-id="c9623-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c9623-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c9623-116">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c9623-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="c9623-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="c9623-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c9623-118">Nowy AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="c9623-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="c9623-119">Tworzy sieć wirtualna platformy Azure i podsieci frontonu.</span><span class="sxs-lookup"><span data-stu-id="c9623-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="c9623-120">Nowe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="c9623-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="c9623-121">Tworzy zaplecza i strefą DMZ podsieci.</span><span class="sxs-lookup"><span data-stu-id="c9623-121">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="c9623-122">Nowe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="c9623-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="c9623-123">Tworzy publicznego adresu IP adres tooaccess hello maszyny Wirtualnej na podstawie hello Internet.</span><span class="sxs-lookup"><span data-stu-id="c9623-123">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="c9623-124">Nowe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="c9623-124">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="c9623-125">Tworzy interfejs sieci wirtualnej i Włącz przesyłanie dalej IP dla niego.</span><span class="sxs-lookup"><span data-stu-id="c9623-125">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="c9623-126">Nowe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="c9623-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="c9623-127">Tworzy sieciową grupę zabezpieczeń (NSG).</span><span class="sxs-lookup"><span data-stu-id="c9623-127">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="c9623-128">Nowe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="c9623-128">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="c9623-129">Tworzy reguły NSG, które zezwala na portach HTTP i HTTPS ruchu przychodzącego toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c9623-129">Creates NSG rules that allow HTTP and HTTPS ports inbound toohello VM.</span></span> |
| [<span data-ttu-id="c9623-130">Zestaw AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="c9623-130">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| <span data-ttu-id="c9623-131">Grupy NSG hello stowarzyszonych i toosubnets tabele tras.</span><span class="sxs-lookup"><span data-stu-id="c9623-131">Associates hello NSGs and route tables toosubnets.</span></span> |
| [<span data-ttu-id="c9623-132">Nowe AzureRmRouteTable</span><span class="sxs-lookup"><span data-stu-id="c9623-132">New-AzureRmRouteTable</span></span>](/powershell/module/azurerm.network/new-azurermroutetable)| <span data-ttu-id="c9623-133">Tworzy tabelę tras dla wszystkich tras.</span><span class="sxs-lookup"><span data-stu-id="c9623-133">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="c9623-134">Nowe AzureRMRouteConfig</span><span class="sxs-lookup"><span data-stu-id="c9623-134">New-AzureRMRouteConfig</span></span>](/powershell/module/azurerm.network/new-azurermrouteconfig)| <span data-ttu-id="c9623-135">Tworzy tras tooroute ruch między podsieciami i hello Internet za pośrednictwem hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c9623-135">Creates routes tooroute traffic between subnets and hello Internet through hello VM.</span></span> |
| [<span data-ttu-id="c9623-136">Nowe AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="c9623-136">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="c9623-137">Tworzy maszynę wirtualną i dołącza hello tooit karty Sieciowej.</span><span class="sxs-lookup"><span data-stu-id="c9623-137">Creates a virtual machine and attaches hello NIC tooit.</span></span> <span data-ttu-id="c9623-138">To polecenie określa również toouse obrazu maszyny wirtualnej hello i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="c9623-138">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="c9623-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c9623-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | <span data-ttu-id="c9623-140">Usuwa grupę zasobów i wszystkie zasoby, które zawiera.</span><span class="sxs-lookup"><span data-stu-id="c9623-140">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c9623-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c9623-141">Next steps</span></span>

<span data-ttu-id="c9623-142">Aby uzyskać więcej informacji na powitania programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c9623-142">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="c9623-143">Dodatkowe przykłady skryptów PowerShell sieci można znaleźć w hello [Azure Przegląd dokumentacji](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c9623-143">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
