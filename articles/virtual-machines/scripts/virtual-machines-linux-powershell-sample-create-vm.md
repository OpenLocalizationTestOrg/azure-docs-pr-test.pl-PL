---
title: "aaaAzure przykładowy skrypt programu PowerShell — Utwórz Maszynę wirtualną systemu Linux | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — Utwórz Maszynę wirtualną systemu Linux"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 8ee2ee42aa68ee135a859b7eaead25811cf54095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-configured-virtual-machine-with-powershell"></a><span data-ttu-id="5a3f6-103">Utwórz maszynę wirtualną w pełni skonfigurowany przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a3f6-103">Create a fully configured virtual machine with PowerShell</span></span>

<span data-ttu-id="5a3f6-104">Ten skrypt tworzy maszynę wirtualną platformy Azure z systemem operacyjnym Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span></span> <span data-ttu-id="5a3f6-105">Po uruchomieniu skryptu hello, można uzyskać dostępu do maszyny wirtualnej hello za pomocą protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-105">After running hello script, you can access hello virtual machine over SSH.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5a3f6-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="5a3f6-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.ps1 "Create VM detailed")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5a3f6-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="5a3f6-107">Clean up deployment</span></span> 

<span data-ttu-id="5a3f6-108">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5a3f6-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="5a3f6-109">Script explanation</span></span>

<span data-ttu-id="5a3f6-110">Ten skrypt używa hello następujące polecenia toocreate hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="5a3f6-111">Każdy element w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5a3f6-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="5a3f6-112">Command</span></span> | <span data-ttu-id="5a3f6-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="5a3f6-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5a3f6-114">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5a3f6-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5a3f6-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5a3f6-116">Nowe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5a3f6-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5a3f6-117">Tworzy konfiguracji podsieci.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-117">Creates a subnet configuration.</span></span> <span data-ttu-id="5a3f6-118">Ta konfiguracja jest używana z procesu tworzenia hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="5a3f6-119">Nowy AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="5a3f6-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="5a3f6-120">Tworzy sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="5a3f6-121">Nowe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="5a3f6-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="5a3f6-122">Tworzy publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="5a3f6-123">Nowe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="5a3f6-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="5a3f6-124">Tworzy konfiguracji reguły grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="5a3f6-125">Ta konfiguracja jest używane toocreate reguły NSG, po utworzeniu hello NSG.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="5a3f6-126">Nowe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="5a3f6-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="5a3f6-127">Tworzy sieciową grupę zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="5a3f6-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5a3f6-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5a3f6-129">Pobiera informacje o podsieci.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-129">Gets subnet information.</span></span> <span data-ttu-id="5a3f6-130">Te informacje jest używany podczas tworzenia interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="5a3f6-131">Nowe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="5a3f6-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="5a3f6-132">Tworzy interfejs sieciowy.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="5a3f6-133">Nowe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="5a3f6-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="5a3f6-134">Tworzy konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-134">Creates a VM configuration.</span></span> <span data-ttu-id="5a3f6-135">Ta konfiguracja zawiera informacje, takie jak nazwa maszyny Wirtualnej, system operacyjny i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="5a3f6-136">Konfiguracja Hello jest używany podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="5a3f6-137">Nowe AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="5a3f6-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="5a3f6-138">Utwórz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-138">Create a virtual machine.</span></span> |
|[<span data-ttu-id="5a3f6-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5a3f6-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="5a3f6-140">Usuwa grupę zasobów i wszystkie zasoby zawarte w ciągu.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-140">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5a3f6-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5a3f6-141">Next steps</span></span>

<span data-ttu-id="5a3f6-142">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5a3f6-142">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5a3f6-143">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5a3f6-143">Additional virtual machine PowerShell script samples can be found in hello [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
