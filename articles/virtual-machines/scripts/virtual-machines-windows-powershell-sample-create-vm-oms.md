---
title: "Przykładowy skrypt programu PowerShell Azure - OMS | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure - OMS"
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
ms.date: 03/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 9f876be46f5214b12d6a46e54509ba3541f819c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-operations-management-suite-monitored-vm-with-powershell"></a><span data-ttu-id="f6811-103">Utwórz maszynę Wirtualną za pomocą programu PowerShell monitorowane Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="f6811-103">Create an Operations Management Suite monitored VM with PowerShell</span></span>

<span data-ttu-id="f6811-104">Ten skrypt tworzy maszynę wirtualną platformy Azure, zainstalowanie agenta programu Operations Management Suite (OMS) i rejestruje system z obszarem roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="f6811-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="f6811-105">Po uruchomieniu skryptu, maszyny wirtualne będą widoczne w konsoli OMS.</span><span class="sxs-lookup"><span data-stu-id="f6811-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span> <span data-ttu-id="f6811-106">Ponadto należy zaktualizować obszar roboczy OMS klucza identyfikator i obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="f6811-106">Also, you need to update the OMS workspace ID and workspace key.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f6811-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="f6811-107">Sample script</span></span>

<span data-ttu-id="f6811-108">[!code-powershell[główne](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "OMS tworzenia maszyny Wirtualnej")]</span><span class="sxs-lookup"><span data-stu-id="f6811-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "Create VM OMS")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="f6811-109">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="f6811-109">Clean up deployment</span></span> 

<span data-ttu-id="f6811-110">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="f6811-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f6811-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="f6811-111">Script explanation</span></span>

<span data-ttu-id="f6811-112">Ten skrypt używa następujących poleceń w celu utworzenia wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="f6811-112">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="f6811-113">Każdy element w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="f6811-113">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f6811-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="f6811-114">Command</span></span> | <span data-ttu-id="f6811-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="f6811-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f6811-116">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f6811-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f6811-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="f6811-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f6811-118">Nowe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="f6811-118">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="f6811-119">Tworzy konfiguracji podsieci.</span><span class="sxs-lookup"><span data-stu-id="f6811-119">Creates a subnet configuration.</span></span> <span data-ttu-id="f6811-120">Ta konfiguracja jest używana z procesu tworzenia sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f6811-120">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="f6811-121">Nowy AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="f6811-121">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="f6811-122">Tworzy sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="f6811-122">Creates a virtual network.</span></span> |
| [<span data-ttu-id="f6811-123">Nowe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="f6811-123">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="f6811-124">Tworzy publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="f6811-124">Creates a public IP address.</span></span> |
| [<span data-ttu-id="f6811-125">Nowe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="f6811-125">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="f6811-126">Tworzy konfiguracji reguły grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="f6811-126">Creates a network security group rule configuration.</span></span> <span data-ttu-id="f6811-127">Ta konfiguracja jest używana do utworzenia reguły NSG, gdy grupa NSG jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="f6811-127">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="f6811-128">Nowe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="f6811-128">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="f6811-129">Tworzy sieciową grupę zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="f6811-129">Creates a network security group.</span></span> |
| [<span data-ttu-id="f6811-130">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="f6811-130">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="f6811-131">Pobiera informacje o podsieci.</span><span class="sxs-lookup"><span data-stu-id="f6811-131">Gets subnet information.</span></span> <span data-ttu-id="f6811-132">Te informacje jest używany podczas tworzenia interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="f6811-132">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="f6811-133">Nowe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="f6811-133">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="f6811-134">Tworzy interfejs sieciowy.</span><span class="sxs-lookup"><span data-stu-id="f6811-134">Creates a network interface.</span></span> |
| [<span data-ttu-id="f6811-135">Nowe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="f6811-135">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="f6811-136">Tworzy konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f6811-136">Creates a VM configuration.</span></span> <span data-ttu-id="f6811-137">Ta konfiguracja zawiera informacje, takie jak nazwa maszyny Wirtualnej, system operacyjny i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="f6811-137">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="f6811-138">Konfiguracja jest używany podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f6811-138">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="f6811-139">Nowe AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="f6811-139">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="f6811-140">Utwórz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="f6811-140">Create a virtual machine.</span></span> |
| [<span data-ttu-id="f6811-141">Zestaw AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="f6811-141">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="f6811-142">Dodaj rozszerzenie maszyny Wirtualnej do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f6811-142">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="f6811-143">W takim przypadku rozszerzenie agenta Operations Management Suite jest używane do instalowania agenta pakietu OMS i rejestrowania maszyn wirtualnych w obszarze roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="f6811-143">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
|[<span data-ttu-id="f6811-144">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f6811-144">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="f6811-145">Usuwa grupę zasobów i wszystkie zasoby zawarte w ciągu.</span><span class="sxs-lookup"><span data-stu-id="f6811-145">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f6811-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f6811-146">Next steps</span></span>

<span data-ttu-id="f6811-147">Aby uzyskać więcej informacji dotyczących modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f6811-147">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f6811-148">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w [dokumentacji maszyny Wirtualnej systemu Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f6811-148">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
