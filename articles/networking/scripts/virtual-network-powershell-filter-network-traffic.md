---
title: "Przykładowy skrypt programu PowerShell aaaAzure — ruchu sieciowego maszyn wirtualnych filtru | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — filtrowania ruchu przychodzącego i wychodzącego ruchu sieciowego maszyny Wirtualnej."
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
ms.openlocfilehash: 39eae6a43a8dc7f9fc616ef3ec50f95443fd3547
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="7c1df-103">Filtrowanie ruchu przychodzącego i wychodzącego ruchu sieciowego maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7c1df-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="7c1df-104">Ten przykładowy skrypt tworzy sieć wirtualną z podsieci frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="7c1df-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="7c1df-105">Ruchu przychodzącego ruchu sieciowego podsieci frontonu toohello jest tooHTTP ograniczona, a ruch protokołu HTTPS, gdy wychodzących toohello Internet z podsieci wewnętrznej hello jest niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="7c1df-105">Inbound network traffic toohello front-end subnet is limited tooHTTP, and HTTPS, while outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> <span data-ttu-id="7c1df-106">Po uruchomieniu skryptu hello, będziesz mieć jedną maszynę wirtualną z dwiema kartami sieciowymi.</span><span class="sxs-lookup"><span data-stu-id="7c1df-106">After running hello script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="7c1df-107">Poszczególne karty Sieciowe są połączone tooa innej podsieci.</span><span class="sxs-lookup"><span data-stu-id="7c1df-107">Each NIC is connected tooa different subnet.</span></span>

<span data-ttu-id="7c1df-108">W razie potrzeby zainstaluj hello Azure PowerShell przy użyciu instrukcji hello znalezione w hello [Przewodnik programu Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), a następnie uruchom `Login-AzureRmAccount` toocreate połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="7c1df-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="7c1df-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="7c1df-109">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/filter-network-traffic/filter-network-traffic.ps1  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7c1df-110">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="7c1df-110">Clean up deployment</span></span> 

<span data-ttu-id="7c1df-111">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="7c1df-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="7c1df-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="7c1df-112">Script explanation</span></span>

<span data-ttu-id="7c1df-113">Ten skrypt używa powitania po toocreate poleceń, grupy zasobów, sieci wirtualnej i grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="7c1df-113">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="7c1df-114">Każde polecenie w dokumentacji konkretnego toocommand łącza tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="7c1df-114">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="7c1df-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="7c1df-115">Command</span></span> | <span data-ttu-id="7c1df-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="7c1df-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7c1df-117">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7c1df-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="7c1df-118">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="7c1df-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7c1df-119">Nowe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="7c1df-119">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="7c1df-120">Tworzy obiekt konfiguracji podsieci</span><span class="sxs-lookup"><span data-stu-id="7c1df-120">Creates a subnet configuration object</span></span> |
| [<span data-ttu-id="7c1df-121">Nowy AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="7c1df-121">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="7c1df-122">Tworzy sieć wirtualna platformy Azure i podsieci frontonu.</span><span class="sxs-lookup"><span data-stu-id="7c1df-122">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="7c1df-123">Nowe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="7c1df-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="7c1df-124">Tworzy toobe reguły zabezpieczeń przypisane tooa sieciowej grupy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="7c1df-124">Creates security rules toobe assigned tooa network security group.</span></span> |
| [<span data-ttu-id="7c1df-125">Nowe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="7c1df-125">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) |<span data-ttu-id="7c1df-126">Tworzy reguły NSG, które zezwala lub blokuje określone porty toospecific podsieci.</span><span class="sxs-lookup"><span data-stu-id="7c1df-126">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="7c1df-127">Zestaw AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="7c1df-127">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="7c1df-128">Kojarzy toosubnets grup NSG.</span><span class="sxs-lookup"><span data-stu-id="7c1df-128">Associates NSGs toosubnets.</span></span> |
| [<span data-ttu-id="7c1df-129">Nowe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="7c1df-129">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="7c1df-130">Tworzy publicznego adresu IP adres tooaccess hello maszyny Wirtualnej na podstawie hello Internet.</span><span class="sxs-lookup"><span data-stu-id="7c1df-130">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="7c1df-131">Nowe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="7c1df-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="7c1df-132">Tworzy interfejsy sieci wirtualnej i dołącza je podsieci sieci wirtualnej toohello frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="7c1df-132">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="7c1df-133">Nowe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="7c1df-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="7c1df-134">Tworzy konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7c1df-134">Creates a VM configuration.</span></span> <span data-ttu-id="7c1df-135">Ta konfiguracja zawiera informacje, takie jak nazwa maszyny Wirtualnej, system operacyjny i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="7c1df-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="7c1df-136">Konfiguracja Hello jest używany podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7c1df-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="7c1df-137">Nowe AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="7c1df-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="7c1df-138">Utwórz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="7c1df-138">Create a virtual machine.</span></span> |
|[<span data-ttu-id="7c1df-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7c1df-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="7c1df-140">Usuwa grupę zasobów i wszystkie zasoby zawarte w ciągu.</span><span class="sxs-lookup"><span data-stu-id="7c1df-140">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7c1df-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7c1df-141">Next steps</span></span>

<span data-ttu-id="7c1df-142">Aby uzyskać więcej informacji na powitania programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7c1df-142">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="7c1df-143">Dodatkowe przykłady skryptów PowerShell sieci można znaleźć w hello [Azure Przegląd dokumentacji](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7c1df-143">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
