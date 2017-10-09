---
title: "aaaAzure przykładowy skrypt programu PowerShell — tworzenie NLB maszyny Wirtualnej z systemem Windows | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 60a48c5f243c8ff3ab886437ae45b21ce069ea4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-between-highly-available-virtual-machines"></a><span data-ttu-id="1d52d-103">Ruch Równoważenie obciążenia między maszynami wirtualnymi wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="1d52d-103">Load balance traffic between highly available virtual machines</span></span>

<span data-ttu-id="1d52d-104">Ten przykładowy skrypt tworzy wszystko, co jest potrzebne toorun kilka maszyn wirtualnych systemu Windows Server 2016 skonfigurowany w wysokiej dostępności i załadować zrównoważonym konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1d52d-104">This script sample creates everything needed toorun several Windows Server 2016 virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="1d52d-105">Po uruchamianie skryptu hello, będzie mieć trzy maszyny wirtualne, połączone tooan zestawu dostępności Azure i jest dostępny za pośrednictwem usługi równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="1d52d-105">After running hello script, you will have three virtual machines, joined tooan Azure Availability Set, and accessible through an Azure Load Balancer.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1d52d-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="1d52d-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Create VM NLB")]

## <a name="clean-up-deployment"></a><span data-ttu-id="1d52d-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="1d52d-107">Clean up deployment</span></span> 

<span data-ttu-id="1d52d-108">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="1d52d-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="1d52d-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="1d52d-109">Script explanation</span></span>

<span data-ttu-id="1d52d-110">Ten skrypt używa hello następujące polecenia toocreate hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="1d52d-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="1d52d-111">Każdy element w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="1d52d-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1d52d-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="1d52d-112">Command</span></span> | <span data-ttu-id="1d52d-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="1d52d-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1d52d-114">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1d52d-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="1d52d-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="1d52d-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1d52d-116">Nowe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="1d52d-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="1d52d-117">Tworzy konfiguracji podsieci.</span><span class="sxs-lookup"><span data-stu-id="1d52d-117">Creates a subnet configuration.</span></span> <span data-ttu-id="1d52d-118">Ta konfiguracja jest używana z procesu tworzenia hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1d52d-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="1d52d-119">Nowy AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="1d52d-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="1d52d-120">Tworzy sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="1d52d-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="1d52d-121">Nowe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="1d52d-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="1d52d-122">Tworzy publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="1d52d-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="1d52d-123">Nowe AzureRmLoadBalancerFrontendIpConfig</span><span class="sxs-lookup"><span data-stu-id="1d52d-123">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="1d52d-124">Tworzy konfigurację IP frontonu modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="1d52d-124">Creates a front-end IP configuration for a load balancer.</span></span> |
| [<span data-ttu-id="1d52d-125">Nowe AzureRmLoadBalancerBackendAddressPoolConfig</span><span class="sxs-lookup"><span data-stu-id="1d52d-125">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="1d52d-126">Tworzy Konfiguracja puli adresów zaplecza, usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="1d52d-126">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="1d52d-127">Nowe AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="1d52d-127">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="1d52d-128">Tworzy sondę konfigurację usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="1d52d-128">Creates a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="1d52d-129">Nowe AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="1d52d-129">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="1d52d-130">Tworzy regułę konfigurację usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="1d52d-130">Creates a rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="1d52d-131">Nowe AzureRmLoadBalancerInboundNatRuleConfig</span><span class="sxs-lookup"><span data-stu-id="1d52d-131">New-AzureRmLoadBalancerInboundNatRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | <span data-ttu-id="1d52d-132">Tworzy przychodzących konfiguracji reguły NAT dla modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="1d52d-132">Creates an inbound NAT rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="1d52d-133">Nowe AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="1d52d-133">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="1d52d-134">Tworzy moduł równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="1d52d-134">Creates a load balancer.</span></span> |
| [<span data-ttu-id="1d52d-135">Nowe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="1d52d-135">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="1d52d-136">Tworzy konfiguracji reguły grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="1d52d-136">Creates a network security group rule configuration.</span></span> <span data-ttu-id="1d52d-137">Ta konfiguracja jest używane toocreate reguły NSG, po utworzeniu hello NSG.</span><span class="sxs-lookup"><span data-stu-id="1d52d-137">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="1d52d-138">Nowe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="1d52d-138">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="1d52d-139">Tworzy sieciową grupę zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="1d52d-139">Creates a network security group.</span></span> |
| [<span data-ttu-id="1d52d-140">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="1d52d-140">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="1d52d-141">Pobiera informacje o podsieci.</span><span class="sxs-lookup"><span data-stu-id="1d52d-141">Gets subnet information.</span></span> <span data-ttu-id="1d52d-142">Te informacje jest używany podczas tworzenia interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="1d52d-142">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="1d52d-143">Nowe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="1d52d-143">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="1d52d-144">Tworzy interfejs sieciowy.</span><span class="sxs-lookup"><span data-stu-id="1d52d-144">Creates a network interface.</span></span> |
| [<span data-ttu-id="1d52d-145">Nowe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="1d52d-145">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="1d52d-146">Tworzy konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1d52d-146">Creates a VM configuration.</span></span> <span data-ttu-id="1d52d-147">Ta konfiguracja zawiera informacje, takie jak nazwa maszyny Wirtualnej, system operacyjny i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="1d52d-147">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="1d52d-148">Konfiguracja Hello jest używany podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1d52d-148">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="1d52d-149">Nowe AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="1d52d-149">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="1d52d-150">Utwórz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="1d52d-150">Create a virtual machine.</span></span> |
|[<span data-ttu-id="1d52d-151">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1d52d-151">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="1d52d-152">Usuwa grupę zasobów i wszystkie zasoby zawarte w ciągu.</span><span class="sxs-lookup"><span data-stu-id="1d52d-152">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1d52d-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1d52d-153">Next steps</span></span>

<span data-ttu-id="1d52d-154">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1d52d-154">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="1d52d-155">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1d52d-155">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
