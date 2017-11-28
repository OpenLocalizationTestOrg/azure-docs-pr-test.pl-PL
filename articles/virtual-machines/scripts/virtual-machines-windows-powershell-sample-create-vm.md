---
title: "Skrypt programu PowerShell Azure przykładowe — tworzenie maszyny Wirtualnej systemu Windows | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — tworzenie maszyny Wirtualnej systemu Windows"
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
ms.date: 03/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: a9e46aded0cf3792558a7fba6f00e5662166cc0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-fully-configured-virtual-machine-with-powershell"></a><span data-ttu-id="3ee9b-103">Utwórz maszynę wirtualną w pełni skonfigurowany przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ee9b-103">Create a fully configured virtual machine with PowerShell</span></span>

<span data-ttu-id="3ee9b-104">Ten skrypt tworzy maszynę wirtualną platformy Azure z systemem Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="3ee9b-105">Po uruchomieniu skryptu, można uzyskać dostępu do maszyny wirtualnej za pośrednictwem protokołu RDP.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-105">After running the script, you can access the virtual machine over RDP.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="3ee9b-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="3ee9b-106">Sample script</span></span>

<span data-ttu-id="3ee9b-107">[!code-powershell[główne](../../../powershell_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.ps1 "Utwórz maszynę Wirtualną szczegółowe")]</span><span class="sxs-lookup"><span data-stu-id="3ee9b-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.ps1 "Create VM detailed")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="3ee9b-108">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="3ee9b-108">Clean up deployment</span></span> 

<span data-ttu-id="3ee9b-109">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="3ee9b-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="3ee9b-110">Script explanation</span></span>

<span data-ttu-id="3ee9b-111">Ten skrypt używa następujących poleceń w celu utworzenia wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="3ee9b-112">Każdy element w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3ee9b-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="3ee9b-113">Command</span></span> | <span data-ttu-id="3ee9b-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="3ee9b-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3ee9b-115">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3ee9b-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="3ee9b-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3ee9b-117">Nowe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="3ee9b-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="3ee9b-118">Tworzy konfiguracji podsieci.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-118">Creates a subnet configuration.</span></span> <span data-ttu-id="3ee9b-119">Ta konfiguracja jest używana z procesu tworzenia sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="3ee9b-120">Nowy AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="3ee9b-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="3ee9b-121">Tworzy sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="3ee9b-122">Nowe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="3ee9b-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="3ee9b-123">Tworzy publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="3ee9b-124">Nowe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="3ee9b-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="3ee9b-125">Tworzy konfiguracji reguły grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="3ee9b-126">Ta konfiguracja jest używana do utworzenia reguły NSG, gdy grupa NSG jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-126">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="3ee9b-127">Nowe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="3ee9b-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="3ee9b-128">Tworzy sieciową grupę zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="3ee9b-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="3ee9b-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="3ee9b-130">Pobiera informacje o podsieci.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-130">Gets subnet information.</span></span> <span data-ttu-id="3ee9b-131">Te informacje jest używany podczas tworzenia interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="3ee9b-132">Nowe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="3ee9b-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="3ee9b-133">Tworzy interfejs sieciowy.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="3ee9b-134">Nowe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="3ee9b-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="3ee9b-135">Tworzy konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-135">Creates a VM configuration.</span></span> <span data-ttu-id="3ee9b-136">Ta konfiguracja zawiera informacje, takie jak nazwa maszyny Wirtualnej, system operacyjny i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="3ee9b-137">Konfiguracja jest używany podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="3ee9b-138">Nowe AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="3ee9b-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="3ee9b-139">Utwórz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-139">Create a virtual machine.</span></span> |
|[<span data-ttu-id="3ee9b-140">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3ee9b-140">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="3ee9b-141">Usuwa grupę zasobów i wszystkie zasoby zawarte w ciągu.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-141">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3ee9b-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3ee9b-142">Next steps</span></span>

<span data-ttu-id="3ee9b-143">Aby uzyskać więcej informacji dotyczących modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3ee9b-143">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="3ee9b-144">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w [dokumentacji maszyny Wirtualnej systemu Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3ee9b-144">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
