---
title: "Skrypt programu PowerShell Azure przykładowe — tworzenie NLB maszyny Wirtualnej z systemem Windows | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — tworzenie NLB maszyny Wirtualnej systemu Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 25bcbbcd1615e01a384825d7bd1582a528e91f71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="load-balance-traffic-between-highly-available-virtual-machines"></a><span data-ttu-id="ac0e5-103">Ruch Równoważenie obciążenia między maszynami wirtualnymi wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="ac0e5-103">Load balance traffic between highly available virtual machines</span></span>

<span data-ttu-id="ac0e5-104">Ten przykładowy skrypt tworzy wszystko, co jest potrzebne do uruchomienia wielu maszyn wirtualnych systemu Windows Server 2016 skonfigurowane w wysokiej dostępności i konfiguracji z równoważeniem obciążenia.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-104">This script sample creates everything needed to run several Windows Server 2016 virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="ac0e5-105">Po uruchomieniu skryptu ma trzy maszyny wirtualne, dołączony do zestawu dostępności Azure i jest dostępny za pośrednictwem usługi równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-105">After running the script, you will have three virtual machines, joined to an Azure Availability Set, and accessible through an Azure Load Balancer.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ac0e5-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="ac0e5-106">Sample script</span></span>

<span data-ttu-id="ac0e5-107">[!code-powershell[główne](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "utworzyć równoważenia obciążenia Sieciowego maszyny Wirtualnej")]</span><span class="sxs-lookup"><span data-stu-id="ac0e5-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Create VM NLB")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="ac0e5-108">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="ac0e5-108">Clean up deployment</span></span> 

<span data-ttu-id="ac0e5-109">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ac0e5-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="ac0e5-110">Script explanation</span></span>

<span data-ttu-id="ac0e5-111">Ten skrypt używa następujących poleceń w celu utworzenia wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="ac0e5-112">Każdy element w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ac0e5-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="ac0e5-113">Command</span></span> | <span data-ttu-id="ac0e5-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="ac0e5-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ac0e5-115">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ac0e5-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="ac0e5-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ac0e5-117">Nowe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="ac0e5-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="ac0e5-118">Tworzy konfiguracji podsieci.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-118">Creates a subnet configuration.</span></span> <span data-ttu-id="ac0e5-119">Ta konfiguracja jest używana z procesu tworzenia sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="ac0e5-120">Nowy AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="ac0e5-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="ac0e5-121">Tworzy sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="ac0e5-122">Nowe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="ac0e5-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="ac0e5-123">Tworzy publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="ac0e5-124">Nowe AzureRmLoadBalancerFrontendIpConfig</span><span class="sxs-lookup"><span data-stu-id="ac0e5-124">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="ac0e5-125">Tworzy konfigurację IP frontonu modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-125">Creates a front-end IP configuration for a load balancer.</span></span> |
| [<span data-ttu-id="ac0e5-126">Nowe AzureRmLoadBalancerBackendAddressPoolConfig</span><span class="sxs-lookup"><span data-stu-id="ac0e5-126">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="ac0e5-127">Tworzy Konfiguracja puli adresów zaplecza, usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-127">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="ac0e5-128">Nowe AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="ac0e5-128">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="ac0e5-129">Tworzy sondę konfigurację usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-129">Creates a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="ac0e5-130">Nowe AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="ac0e5-130">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="ac0e5-131">Tworzy regułę konfigurację usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-131">Creates a rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="ac0e5-132">Nowe AzureRmLoadBalancerInboundNatRuleConfig</span><span class="sxs-lookup"><span data-stu-id="ac0e5-132">New-AzureRmLoadBalancerInboundNatRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | <span data-ttu-id="ac0e5-133">Tworzy przychodzących konfiguracji reguły NAT dla modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-133">Creates an inbound NAT rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="ac0e5-134">Nowe AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="ac0e5-134">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="ac0e5-135">Tworzy moduł równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-135">Creates a load balancer.</span></span> |
| [<span data-ttu-id="ac0e5-136">Nowe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="ac0e5-136">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="ac0e5-137">Tworzy konfiguracji reguły grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-137">Creates a network security group rule configuration.</span></span> <span data-ttu-id="ac0e5-138">Ta konfiguracja jest używana do utworzenia reguły NSG, gdy grupa NSG jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-138">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="ac0e5-139">Nowe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="ac0e5-139">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="ac0e5-140">Tworzy sieciową grupę zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-140">Creates a network security group.</span></span> |
| [<span data-ttu-id="ac0e5-141">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="ac0e5-141">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="ac0e5-142">Pobiera informacje o podsieci.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-142">Gets subnet information.</span></span> <span data-ttu-id="ac0e5-143">Te informacje jest używany podczas tworzenia interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-143">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="ac0e5-144">Nowe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="ac0e5-144">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="ac0e5-145">Tworzy interfejs sieciowy.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-145">Creates a network interface.</span></span> |
| [<span data-ttu-id="ac0e5-146">Nowe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="ac0e5-146">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="ac0e5-147">Tworzy konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-147">Creates a VM configuration.</span></span> <span data-ttu-id="ac0e5-148">Ta konfiguracja zawiera informacje, takie jak nazwa maszyny Wirtualnej, system operacyjny i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-148">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="ac0e5-149">Konfiguracja jest używany podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-149">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="ac0e5-150">Nowe AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="ac0e5-150">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="ac0e5-151">Utwórz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-151">Create a virtual machine.</span></span> |
|[<span data-ttu-id="ac0e5-152">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ac0e5-152">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="ac0e5-153">Usuwa grupę zasobów i wszystkie zasoby zawarte w ciągu.</span><span class="sxs-lookup"><span data-stu-id="ac0e5-153">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ac0e5-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ac0e5-154">Next steps</span></span>

<span data-ttu-id="ac0e5-155">Aby uzyskać więcej informacji dotyczących modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ac0e5-155">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ac0e5-156">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w [dokumentacji maszyny Wirtualnej systemu Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ac0e5-156">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
