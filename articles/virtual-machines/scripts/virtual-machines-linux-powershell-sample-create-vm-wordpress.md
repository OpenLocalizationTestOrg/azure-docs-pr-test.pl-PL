---
title: "aaaAzure przykładowy skrypt programu PowerShell - WordPress | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure - WordPress"
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
ms.date: 03/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b011726a772bb4d13fcfcba088eac4d0305967c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-wordpress-vm-with-powershell"></a><span data-ttu-id="5e097-103">Tworzenie maszyny Wirtualnej WordPress przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e097-103">Create a WordPress VM with PowerShell</span></span>

<span data-ttu-id="5e097-104">Ten skrypt tworzy maszynę wirtualną i używa hello maszyny wirtualnej Azure skryptu niestandardowego rozszerzenia tooinstall WordPress.</span><span class="sxs-lookup"><span data-stu-id="5e097-104">This script creates a virtual machine and uses hello Azure Virtual Machine custom script extension tooinstall WordPress.</span></span> <span data-ttu-id="5e097-105">Po uruchamianie skryptu hello, można uzyskać dostępu do hello WordPress konfiguracji witryny na `http://<public IP of VM>/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="5e097-105">After running hello script, you can access hello WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5e097-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="5e097-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.ps1 "Create VM WordPress")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5e097-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="5e097-107">Clean up deployment</span></span> 

<span data-ttu-id="5e097-108">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="5e097-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5e097-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="5e097-109">Script explanation</span></span>

<span data-ttu-id="5e097-110">Ten skrypt używa hello następujące polecenia toocreate hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="5e097-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="5e097-111">Każdy element w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="5e097-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5e097-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="5e097-112">Command</span></span> | <span data-ttu-id="5e097-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="5e097-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5e097-114">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5e097-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5e097-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="5e097-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5e097-116">Nowe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5e097-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5e097-117">Tworzy konfiguracji podsieci.</span><span class="sxs-lookup"><span data-stu-id="5e097-117">Creates a subnet configuration.</span></span> <span data-ttu-id="5e097-118">Ta konfiguracja jest używana z procesu tworzenia hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5e097-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="5e097-119">Nowy AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="5e097-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="5e097-120">Tworzy sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="5e097-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="5e097-121">Nowe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="5e097-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="5e097-122">Tworzy publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="5e097-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="5e097-123">Nowe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="5e097-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="5e097-124">Tworzy konfiguracji reguły grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="5e097-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="5e097-125">Ta konfiguracja jest używane toocreate reguły NSG, po utworzeniu hello NSG.</span><span class="sxs-lookup"><span data-stu-id="5e097-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="5e097-126">Nowe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="5e097-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="5e097-127">Tworzy sieciową grupę zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="5e097-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="5e097-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5e097-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5e097-129">Pobiera informacje o podsieci.</span><span class="sxs-lookup"><span data-stu-id="5e097-129">Gets subnet information.</span></span> <span data-ttu-id="5e097-130">Te informacje jest używany podczas tworzenia interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="5e097-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="5e097-131">Nowe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="5e097-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="5e097-132">Tworzy interfejs sieciowy.</span><span class="sxs-lookup"><span data-stu-id="5e097-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="5e097-133">Nowe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="5e097-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="5e097-134">Tworzy konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5e097-134">Creates a VM configuration.</span></span> <span data-ttu-id="5e097-135">Ta konfiguracja zawiera informacje, takie jak nazwa maszyny Wirtualnej, system operacyjny i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="5e097-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="5e097-136">Konfiguracja Hello jest używany podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5e097-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="5e097-137">Nowe AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="5e097-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="5e097-138">Utwórz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="5e097-138">Create a virtual machine.</span></span> |
| [<span data-ttu-id="5e097-139">Zestaw AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="5e097-139">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="5e097-140">Dodaj maszynę wirtualną toohello niestandardowe rozszerzenie skryptu hello, która wywołuje skrypt tooinstall WordPress.</span><span class="sxs-lookup"><span data-stu-id="5e097-140">Add hello Custom Script Extension toohello virtual machine, which invokes a script tooinstall WordPress.</span></span> |
|[<span data-ttu-id="5e097-141">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5e097-141">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="5e097-142">Usuwa grupę zasobów i wszystkie zasoby zawarte w ciągu.</span><span class="sxs-lookup"><span data-stu-id="5e097-142">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5e097-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5e097-143">Next steps</span></span>

<span data-ttu-id="5e097-144">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5e097-144">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5e097-145">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5e097-145">Additional virtual machine PowerShell script samples can be found in hello [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
