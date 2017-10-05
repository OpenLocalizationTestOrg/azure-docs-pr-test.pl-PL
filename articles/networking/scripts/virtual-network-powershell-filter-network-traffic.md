---
title: "Przykładowym skrypcie programu PowerShell Azure - ruchu sieciowego maszyn wirtualnych filtr | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: e871ba2f370157936c2aaabc804dc9f5aea6d7ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="5e148-103">Filtrowanie ruchu przychodzącego i wychodzącego ruchu sieciowego maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="5e148-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="5e148-104">Ten przykładowy skrypt tworzy sieć wirtualną z podsieci frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="5e148-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="5e148-105">Ruch sieciowy przychodzący do podsieci frontonu może zawierać maksymalnie HTTP i HTTPS, gdy ruch wychodzący do Internetu z podsieci wewnętrznej jest niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="5e148-105">Inbound network traffic to the front-end subnet is limited to HTTP, and HTTPS, while outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> <span data-ttu-id="5e148-106">Po uruchomieniu skryptu, ma jedną maszynę wirtualną z dwiema kartami sieciowymi.</span><span class="sxs-lookup"><span data-stu-id="5e148-106">After running the script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="5e148-107">Każda karta sieciowa jest podłączona do innej podsieci.</span><span class="sxs-lookup"><span data-stu-id="5e148-107">Each NIC is connected to a different subnet.</span></span>

<span data-ttu-id="5e148-108">W razie potrzeby zainstalować program Azure PowerShell przy użyciu instrukcji w [Przewodnik programu Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), a następnie uruchom `Login-AzureRmAccount` można utworzyć połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="5e148-108">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5e148-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="5e148-109">Sample script</span></span>


<span data-ttu-id="5e148-110">[!code-powershell[główne](../../../powershell_scripts/virtual-network/filter-network-traffic/filter-network-traffic.ps1  "ruchu sieciowego maszyn wirtualnych filtru")]</span><span class="sxs-lookup"><span data-stu-id="5e148-110">[!code-powershell[main](../../../powershell_scripts/virtual-network/filter-network-traffic/filter-network-traffic.ps1  "Filter VM network traffic")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5e148-111">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="5e148-111">Clean up deployment</span></span> 

<span data-ttu-id="5e148-112">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="5e148-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5e148-113">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="5e148-113">Script explanation</span></span>

<span data-ttu-id="5e148-114">Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, sieć wirtualną i grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="5e148-114">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="5e148-115">Każde polecenie w tabeli łącza do dokumentacji specyficzne dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="5e148-115">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="5e148-116">Polecenie</span><span class="sxs-lookup"><span data-stu-id="5e148-116">Command</span></span> | <span data-ttu-id="5e148-117">Uwagi</span><span class="sxs-lookup"><span data-stu-id="5e148-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5e148-118">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5e148-118">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5e148-119">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="5e148-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5e148-120">Nowe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5e148-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5e148-121">Tworzy obiekt konfiguracji podsieci</span><span class="sxs-lookup"><span data-stu-id="5e148-121">Creates a subnet configuration object</span></span> |
| [<span data-ttu-id="5e148-122">Nowy AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="5e148-122">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="5e148-123">Tworzy sieć wirtualna platformy Azure i podsieci frontonu.</span><span class="sxs-lookup"><span data-stu-id="5e148-123">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="5e148-124">Nowe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="5e148-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="5e148-125">Tworzy zasady zabezpieczeń ma być przypisany do grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="5e148-125">Creates security rules to be assigned to a network security group.</span></span> |
| [<span data-ttu-id="5e148-126">Nowe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="5e148-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) |<span data-ttu-id="5e148-127">Tworzy reguły NSG, które zezwala lub blokuje określone porty do określonych podsieci.</span><span class="sxs-lookup"><span data-stu-id="5e148-127">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="5e148-128">Zestaw AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5e148-128">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5e148-129">Kojarzy grup NSG do podsieci.</span><span class="sxs-lookup"><span data-stu-id="5e148-129">Associates NSGs to subnets.</span></span> |
| [<span data-ttu-id="5e148-130">Nowe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="5e148-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="5e148-131">Tworzy publiczny adres IP na dostęp do maszyny Wirtualnej z Internetu.</span><span class="sxs-lookup"><span data-stu-id="5e148-131">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="5e148-132">Nowe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="5e148-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="5e148-133">Tworzy interfejsy sieci wirtualnej i dołącza je do podsieci sieci wirtualnej frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="5e148-133">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="5e148-134">Nowe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="5e148-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="5e148-135">Tworzy konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5e148-135">Creates a VM configuration.</span></span> <span data-ttu-id="5e148-136">Ta konfiguracja zawiera informacje, takie jak nazwa maszyny Wirtualnej, system operacyjny i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="5e148-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="5e148-137">Konfiguracja jest używany podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5e148-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="5e148-138">Nowe AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="5e148-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="5e148-139">Utwórz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="5e148-139">Create a virtual machine.</span></span> |
|[<span data-ttu-id="5e148-140">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5e148-140">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="5e148-141">Usuwa grupę zasobów i wszystkie zasoby zawarte w ciągu.</span><span class="sxs-lookup"><span data-stu-id="5e148-141">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5e148-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5e148-142">Next steps</span></span>

<span data-ttu-id="5e148-143">Aby uzyskać więcej informacji dotyczących programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5e148-143">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="5e148-144">Dodatkowe przykłady skryptów PowerShell sieci można znaleźć w [Azure Przegląd dokumentacji](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5e148-144">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>