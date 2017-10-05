---
title: "Przykładowy skrypt programu PowerShell Azure - OMS | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure - OMS"
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
ms.openlocfilehash: cd23f71221efb62d2547b2b683ca8e2218403a2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-operations-management-suite-monitored-vm-with-powershell"></a><span data-ttu-id="b3ded-103">Utwórz maszynę Wirtualną za pomocą programu PowerShell monitorowane Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="b3ded-103">Create an Operations Management Suite monitored VM with PowerShell</span></span>

<span data-ttu-id="b3ded-104">Ten skrypt tworzy maszynę wirtualną platformy Azure, zainstalowanie agenta programu Operations Management Suite (OMS) i rejestruje system z obszarem roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="b3ded-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="b3ded-105">Po uruchomieniu skryptu, maszyny wirtualne będą widoczne w konsoli OMS.</span><span class="sxs-lookup"><span data-stu-id="b3ded-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b3ded-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="b3ded-106">Sample script</span></span>

<span data-ttu-id="b3ded-107">[!code-powershell[główne](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.ps1 "OMS tworzenia maszyny Wirtualnej")]</span><span class="sxs-lookup"><span data-stu-id="b3ded-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.ps1 "Create VM OMS")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="b3ded-108">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="b3ded-108">Clean up deployment</span></span> 

<span data-ttu-id="b3ded-109">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="b3ded-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="b3ded-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="b3ded-110">Script explanation</span></span>

<span data-ttu-id="b3ded-111">Ten skrypt używa następujących poleceń w celu utworzenia wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="b3ded-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="b3ded-112">Każdy element w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="b3ded-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b3ded-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="b3ded-113">Command</span></span> | <span data-ttu-id="b3ded-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b3ded-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b3ded-115">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b3ded-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="b3ded-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="b3ded-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b3ded-117">Nowe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="b3ded-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="b3ded-118">Tworzy konfiguracji podsieci.</span><span class="sxs-lookup"><span data-stu-id="b3ded-118">Creates a subnet configuration.</span></span> <span data-ttu-id="b3ded-119">Ta konfiguracja jest używana z procesu tworzenia sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b3ded-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="b3ded-120">Nowy AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="b3ded-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="b3ded-121">Tworzy sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="b3ded-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="b3ded-122">Nowe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="b3ded-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="b3ded-123">Tworzy publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="b3ded-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="b3ded-124">Nowe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="b3ded-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="b3ded-125">Tworzy konfiguracji reguły grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="b3ded-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="b3ded-126">Ta konfiguracja jest używana do utworzenia reguły NSG, gdy grupa NSG jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="b3ded-126">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="b3ded-127">Nowe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="b3ded-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="b3ded-128">Tworzy sieciową grupę zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="b3ded-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="b3ded-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="b3ded-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="b3ded-130">Pobiera informacje o podsieci.</span><span class="sxs-lookup"><span data-stu-id="b3ded-130">Gets subnet information.</span></span> <span data-ttu-id="b3ded-131">Te informacje jest używany podczas tworzenia interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="b3ded-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="b3ded-132">Nowe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="b3ded-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="b3ded-133">Tworzy interfejs sieciowy.</span><span class="sxs-lookup"><span data-stu-id="b3ded-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="b3ded-134">Nowe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="b3ded-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="b3ded-135">Tworzy konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b3ded-135">Creates a VM configuration.</span></span> <span data-ttu-id="b3ded-136">Ta konfiguracja zawiera informacje, takie jak nazwa maszyny Wirtualnej, system operacyjny i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="b3ded-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="b3ded-137">Konfiguracja jest używany podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b3ded-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="b3ded-138">Nowe AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="b3ded-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="b3ded-139">Utwórz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="b3ded-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="b3ded-140">Zestaw AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="b3ded-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="b3ded-141">Dodaj rozszerzenie maszyny Wirtualnej do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b3ded-141">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="b3ded-142">W takim przypadku rozszerzenie agenta Operations Management Suite jest używane do instalowania agenta pakietu OMS i rejestrowania maszyn wirtualnych w obszarze roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="b3ded-142">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
|[<span data-ttu-id="b3ded-143">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b3ded-143">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="b3ded-144">Usuwa grupę zasobów i wszystkie zasoby zawarte w ciągu.</span><span class="sxs-lookup"><span data-stu-id="b3ded-144">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b3ded-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b3ded-145">Next steps</span></span>

<span data-ttu-id="b3ded-146">Aby uzyskać więcej informacji dotyczących modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b3ded-146">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="b3ded-147">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b3ded-147">Additional virtual machine PowerShell script samples can be found in the [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
