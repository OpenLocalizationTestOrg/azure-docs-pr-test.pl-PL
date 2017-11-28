---
title: "Azure przykładowy skrypt programu PowerShell — kierować ruchem przez urządzenie wirtualne sieci | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 883d28dac72a66c2186d222f72b04d68e532cead
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="5f887-103">Kierować ruchem przez urządzenie wirtualne sieci</span><span class="sxs-lookup"><span data-stu-id="5f887-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="5f887-104">Ten przykładowy skrypt tworzy sieć wirtualną z podsieci frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="5f887-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="5f887-105">Tworzy również Maszynę wirtualną z przekazywanie IP jest włączone, można kierować ruchem między dwiema podsieciami.</span><span class="sxs-lookup"><span data-stu-id="5f887-105">It also creates a VM with IP forwarding enabled to route traffic between the two subnets.</span></span> <span data-ttu-id="5f887-106">Po uruchomieniu skryptu można wdrażać oprogramowanie sieci, takie jak aplikacja zapory, do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5f887-106">After running the script you can deploy network software, such as a firewall application, to the VM.</span></span>

<span data-ttu-id="5f887-107">W razie potrzeby zainstalować program Azure PowerShell przy użyciu instrukcji w [Przewodnik programu Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), a następnie uruchom `Login-AzureRmAccount` można utworzyć połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="5f887-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5f887-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="5f887-108">Sample script</span></span>


<span data-ttu-id="5f887-109">[!code-powershell[główne](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "kierować ruchem przez urządzenie wirtualne sieci")]</span><span class="sxs-lookup"><span data-stu-id="5f887-109">[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5f887-110">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="5f887-110">Clean up deployment</span></span> 

<span data-ttu-id="5f887-111">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="5f887-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a><span data-ttu-id="5f887-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="5f887-112">Script explanation</span></span>

<span data-ttu-id="5f887-113">Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, sieć wirtualną i grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="5f887-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="5f887-114">Każde polecenie w tabeli łącza do dokumentacji specyficzne dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="5f887-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="5f887-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="5f887-115">Command</span></span> | <span data-ttu-id="5f887-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="5f887-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5f887-117">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5f887-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="5f887-118">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="5f887-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5f887-119">Nowy AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="5f887-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="5f887-120">Tworzy sieć wirtualna platformy Azure i podsieci frontonu.</span><span class="sxs-lookup"><span data-stu-id="5f887-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="5f887-121">Nowe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5f887-121">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5f887-122">Tworzy zaplecza i strefą DMZ podsieci.</span><span class="sxs-lookup"><span data-stu-id="5f887-122">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="5f887-123">Nowe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="5f887-123">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="5f887-124">Tworzy publiczny adres IP na dostęp do maszyny Wirtualnej z Internetu.</span><span class="sxs-lookup"><span data-stu-id="5f887-124">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="5f887-125">Nowe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="5f887-125">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="5f887-126">Tworzy interfejs sieci wirtualnej i Włącz przesyłanie dalej IP dla niego.</span><span class="sxs-lookup"><span data-stu-id="5f887-126">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="5f887-127">Nowe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="5f887-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="5f887-128">Tworzy sieciową grupę zabezpieczeń (NSG).</span><span class="sxs-lookup"><span data-stu-id="5f887-128">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="5f887-129">Nowe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="5f887-129">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="5f887-130">Tworzy reguły NSG, które zezwala na portach HTTP i HTTPS ruchu przychodzącego do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5f887-130">Creates NSG rules that allow HTTP and HTTPS ports inbound to the VM.</span></span> |
| [<span data-ttu-id="5f887-131">Zestaw AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5f887-131">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| <span data-ttu-id="5f887-132">Powoduje skojarzenie grupy NSG i tabele tras do podsieci.</span><span class="sxs-lookup"><span data-stu-id="5f887-132">Associates the NSGs and route tables to subnets.</span></span> |
| [<span data-ttu-id="5f887-133">Nowe AzureRmRouteTable</span><span class="sxs-lookup"><span data-stu-id="5f887-133">New-AzureRmRouteTable</span></span>](/powershell/module/azurerm.network/new-azurermroutetable)| <span data-ttu-id="5f887-134">Tworzy tabelę tras dla wszystkich tras.</span><span class="sxs-lookup"><span data-stu-id="5f887-134">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="5f887-135">Nowe AzureRMRouteConfig</span><span class="sxs-lookup"><span data-stu-id="5f887-135">New-AzureRMRouteConfig</span></span>](/powershell/module/azurerm.network/new-azurermrouteconfig)| <span data-ttu-id="5f887-136">Tworzy tras można kierować ruchem między podsieciami i Internetem za pośrednictwem maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5f887-136">Creates routes to route traffic between subnets and the Internet through the VM.</span></span> |
| [<span data-ttu-id="5f887-137">Nowe AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="5f887-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="5f887-138">Tworzy maszynę wirtualną i dołącza do karty Sieciowej.</span><span class="sxs-lookup"><span data-stu-id="5f887-138">Creates a virtual machine and attaches the NIC to it.</span></span> <span data-ttu-id="5f887-139">To polecenie określa również obraz maszyny wirtualnej do użycia i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="5f887-139">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="5f887-140">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5f887-140">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | <span data-ttu-id="5f887-141">Usuwa grupę zasobów i wszystkie zasoby, które zawiera.</span><span class="sxs-lookup"><span data-stu-id="5f887-141">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5f887-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5f887-142">Next steps</span></span>

<span data-ttu-id="5f887-143">Aby uzyskać więcej informacji dotyczących programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5f887-143">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="5f887-144">Dodatkowe przykłady skryptów PowerShell sieci można znaleźć w [Azure Przegląd dokumentacji](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5f887-144">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>