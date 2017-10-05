---
title: "Przykładowy skrypt programu PowerShell Azure - IIS z usługi Konfiguracja DSC | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure - IIS z usługi Konfiguracja DSC"
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
ms.date: 03/01/2017
ms.author: nepeters
ms.openlocfilehash: 38476119c88aa7d4f6578fc1e3756e11951e804a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-iis-vm-with-powershell"></a><span data-ttu-id="c79a4-103">Tworzenie maszyny Wirtualnej usług IIS przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c79a4-103">Create an IIS VM with PowerShell</span></span>

<span data-ttu-id="c79a4-104">Ten skrypt tworzy maszynę wirtualną platformy Azure z systemem Windows Server 2016, a następnie używa rozszerzenia DSC maszyny wirtualnej Azure, aby zainstalować usługi IIS.</span><span class="sxs-lookup"><span data-stu-id="c79a4-104">This script creates an Azure Virtual Machine running Windows Server 2016, and then uses the Azure Virtual Machine DSC Extension to install IIS.</span></span> <span data-ttu-id="c79a4-105">Po uruchomieniu skryptu, można uzyskać dostępu do domyślnej witryny usług IIS na publiczny adres IP maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c79a4-105">After running the script, you can access the default IIS website on the public IP address of the virtual machine.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c79a4-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="c79a4-106">Sample script</span></span>

<span data-ttu-id="c79a4-107">[!code-powershell[główne](../../../powershell_scripts/virtual-machine/create-vm-dsc/create-windows-vm-iis-dsc.ps1 "utworzyć DSC IIS maszyn wirtualnych")]</span><span class="sxs-lookup"><span data-stu-id="c79a4-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-dsc/create-windows-vm-iis-dsc.ps1 "Create VM IIS DSC")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c79a4-108">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="c79a4-108">Clean up deployment</span></span> 

<span data-ttu-id="c79a4-109">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="c79a4-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c79a4-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="c79a4-110">Script explanation</span></span>

<span data-ttu-id="c79a4-111">Ten skrypt używa następujących poleceń w celu utworzenia wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="c79a4-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="c79a4-112">Każdy element w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="c79a4-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c79a4-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="c79a4-113">Command</span></span> | <span data-ttu-id="c79a4-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c79a4-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c79a4-115">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c79a4-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c79a4-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="c79a4-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c79a4-117">Nowe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="c79a4-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="c79a4-118">Tworzy konfiguracji podsieci.</span><span class="sxs-lookup"><span data-stu-id="c79a4-118">Creates a subnet configuration.</span></span> <span data-ttu-id="c79a4-119">Ta konfiguracja jest używana z procesu tworzenia sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c79a4-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="c79a4-120">Nowy AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="c79a4-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="c79a4-121">Tworzy sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="c79a4-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="c79a4-122">Nowe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="c79a4-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="c79a4-123">Tworzy publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="c79a4-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="c79a4-124">Nowe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="c79a4-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="c79a4-125">Tworzy konfiguracji reguły grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="c79a4-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="c79a4-126">Ta konfiguracja jest używana do utworzenia reguły NSG, gdy grupa NSG jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="c79a4-126">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="c79a4-127">Nowe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="c79a4-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="c79a4-128">Tworzy sieciową grupę zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="c79a4-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="c79a4-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="c79a4-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="c79a4-130">Pobiera informacje o podsieci.</span><span class="sxs-lookup"><span data-stu-id="c79a4-130">Gets subnet information.</span></span> <span data-ttu-id="c79a4-131">Te informacje jest używany podczas tworzenia interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="c79a4-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="c79a4-132">Nowe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="c79a4-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="c79a4-133">Tworzy interfejs sieciowy.</span><span class="sxs-lookup"><span data-stu-id="c79a4-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="c79a4-134">Nowe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="c79a4-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="c79a4-135">Tworzy konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c79a4-135">Creates a VM configuration.</span></span> <span data-ttu-id="c79a4-136">Ta konfiguracja zawiera informacje, takie jak nazwa maszyny Wirtualnej, system operacyjny i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="c79a4-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="c79a4-137">Konfiguracja jest używany podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c79a4-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="c79a4-138">Nowe AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="c79a4-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="c79a4-139">Utwórz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="c79a4-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="c79a4-140">Zestaw AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="c79a4-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="c79a4-141">Dodaj rozszerzenie maszyny Wirtualnej do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c79a4-141">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="c79a4-142">W tym przykładzie niestandardowe rozszerzenie skryptu jest używany do instalacji usług IIS.</span><span class="sxs-lookup"><span data-stu-id="c79a4-142">In this sample, the custom script extension is used to install IIS.</span></span> |
|[<span data-ttu-id="c79a4-143">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c79a4-143">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="c79a4-144">Usuwa grupę zasobów i wszystkie zasoby zawarte w ciągu.</span><span class="sxs-lookup"><span data-stu-id="c79a4-144">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c79a4-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c79a4-145">Next steps</span></span>

<span data-ttu-id="c79a4-146">Aby uzyskać więcej informacji dotyczących modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c79a4-146">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c79a4-147">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w [dokumentacji maszyny Wirtualnej systemu Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c79a4-147">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
