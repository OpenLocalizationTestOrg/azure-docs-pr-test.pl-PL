---
title: "aaaAzure przykładowy skrypt programu PowerShell - usług IIS | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure — IIS"
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
ms.custom: mvc
ms.openlocfilehash: 707563e3cce32e667c41ab9ec2392c8f12ef116c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iis-vm-with-powershell"></a><span data-ttu-id="9b52a-103">Tworzenie maszyny Wirtualnej usług IIS przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b52a-103">Create an IIS VM with PowerShell</span></span>

<span data-ttu-id="9b52a-104">Ten skrypt tworzy maszynę wirtualną platformy Azure z systemem Windows Server 2016, a następnie używa hello Azure maszyny wirtualnej niestandardowe rozszerzenie skryptu tooinstall usług IIS.</span><span class="sxs-lookup"><span data-stu-id="9b52a-104">This script creates an Azure Virtual Machine running Windows Server 2016, and then uses hello Azure Virtual Machine Custom Script Extension tooinstall IIS.</span></span> <span data-ttu-id="9b52a-105">Po uruchomieniu skryptu hello, można uzyskać dostępu do hello domyślna witryna sieci Web IIS na publiczny adres IP hello hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9b52a-105">After running hello script, you can access hello default IIS website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9b52a-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="9b52a-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Create VM IIS")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9b52a-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="9b52a-107">Clean up deployment</span></span> 

<span data-ttu-id="9b52a-108">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="9b52a-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="9b52a-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="9b52a-109">Script explanation</span></span>

<span data-ttu-id="9b52a-110">Ten skrypt używa hello następujące polecenia toocreate hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="9b52a-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="9b52a-111">Każdy element w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="9b52a-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9b52a-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="9b52a-112">Command</span></span> | <span data-ttu-id="9b52a-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="9b52a-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9b52a-114">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9b52a-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="9b52a-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="9b52a-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9b52a-116">Nowe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="9b52a-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="9b52a-117">Tworzy konfiguracji podsieci.</span><span class="sxs-lookup"><span data-stu-id="9b52a-117">Creates a subnet configuration.</span></span> <span data-ttu-id="9b52a-118">Ta konfiguracja jest używana z procesu tworzenia hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9b52a-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="9b52a-119">Nowy AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="9b52a-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="9b52a-120">Tworzy sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="9b52a-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="9b52a-121">Nowe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="9b52a-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="9b52a-122">Tworzy publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="9b52a-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="9b52a-123">Nowe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="9b52a-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="9b52a-124">Tworzy konfiguracji reguły grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="9b52a-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="9b52a-125">Ta konfiguracja jest używane toocreate reguły NSG, po utworzeniu hello NSG.</span><span class="sxs-lookup"><span data-stu-id="9b52a-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="9b52a-126">Nowe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="9b52a-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="9b52a-127">Tworzy sieciową grupę zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="9b52a-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="9b52a-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="9b52a-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="9b52a-129">Pobiera informacje o podsieci.</span><span class="sxs-lookup"><span data-stu-id="9b52a-129">Gets subnet information.</span></span> <span data-ttu-id="9b52a-130">Te informacje jest używany podczas tworzenia interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="9b52a-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="9b52a-131">Nowe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="9b52a-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="9b52a-132">Tworzy interfejs sieciowy.</span><span class="sxs-lookup"><span data-stu-id="9b52a-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="9b52a-133">Nowe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="9b52a-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="9b52a-134">Tworzy konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9b52a-134">Creates a VM configuration.</span></span> <span data-ttu-id="9b52a-135">Ta konfiguracja zawiera informacje, takie jak nazwa maszyny Wirtualnej, system operacyjny i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="9b52a-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="9b52a-136">Konfiguracja Hello jest używany podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9b52a-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="9b52a-137">Nowe AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="9b52a-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="9b52a-138">Utwórz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="9b52a-138">Create a virtual machine.</span></span> |
| [<span data-ttu-id="9b52a-139">Zestaw AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="9b52a-139">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="9b52a-140">Dodaj maszynę wirtualną toohello rozszerzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9b52a-140">Add a VM extension toohello virtual machine.</span></span> <span data-ttu-id="9b52a-141">W tym przykładzie hello niestandardowe rozszerzenie skryptu jest używany tooinstall usług IIS.</span><span class="sxs-lookup"><span data-stu-id="9b52a-141">In this sample, hello custom script extension is used tooinstall IIS.</span></span> |
|[<span data-ttu-id="9b52a-142">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9b52a-142">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="9b52a-143">Usuwa grupę zasobów i wszystkie zasoby zawarte w ciągu.</span><span class="sxs-lookup"><span data-stu-id="9b52a-143">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9b52a-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9b52a-144">Next steps</span></span>

<span data-ttu-id="9b52a-145">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9b52a-145">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="9b52a-146">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9b52a-146">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
