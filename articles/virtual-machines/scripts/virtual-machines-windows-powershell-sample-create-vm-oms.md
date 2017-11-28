---
title: "aaaAzure przykładowy skrypt programu PowerShell - OMS | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 1eeafbe743013e97bf3fcefb5ce87f72cb503a4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-operations-management-suite-monitored-vm-with-powershell"></a><span data-ttu-id="5f0d1-103">Utwórz maszynę Wirtualną za pomocą programu PowerShell monitorowane Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="5f0d1-103">Create an Operations Management Suite monitored VM with PowerShell</span></span>

<span data-ttu-id="5f0d1-104">Ten skrypt tworzy maszynę wirtualną platformy Azure, instaluje hello agenta Operations Management Suite (OMS) i rejestruje hello system z obszarem roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="5f0d1-104">This script creates an Azure Virtual Machine, installs hello Operations Management Suite (OMS) agent, and enrolls hello system with an OMS workspace.</span></span> <span data-ttu-id="5f0d1-105">Po uruchomieniu skryptu hello hello maszyny wirtualnej będzie widoczny w konsoli OMS hello.</span><span class="sxs-lookup"><span data-stu-id="5f0d1-105">Once hello script has run, hello virtual machine will be visible in hello OMS console.</span></span> <span data-ttu-id="5f0d1-106">Ponadto należy tooupdate hello OMS klucz obszaru roboczego identyfikator i obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="5f0d1-106">Also, you need tooupdate hello OMS workspace ID and workspace key.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5f0d1-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="5f0d1-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "Create VM OMS")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5f0d1-108">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="5f0d1-108">Clean up deployment</span></span> 

<span data-ttu-id="5f0d1-109">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="5f0d1-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5f0d1-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="5f0d1-110">Script explanation</span></span>

<span data-ttu-id="5f0d1-111">Ten skrypt używa hello następujące polecenia toocreate hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="5f0d1-111">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="5f0d1-112">Każdy element w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="5f0d1-112">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5f0d1-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="5f0d1-113">Command</span></span> | <span data-ttu-id="5f0d1-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="5f0d1-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5f0d1-115">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5f0d1-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5f0d1-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="5f0d1-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5f0d1-117">Nowe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5f0d1-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5f0d1-118">Tworzy konfiguracji podsieci.</span><span class="sxs-lookup"><span data-stu-id="5f0d1-118">Creates a subnet configuration.</span></span> <span data-ttu-id="5f0d1-119">Ta konfiguracja jest używana z procesu tworzenia hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5f0d1-119">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="5f0d1-120">Nowy AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="5f0d1-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="5f0d1-121">Tworzy sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="5f0d1-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="5f0d1-122">Nowe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="5f0d1-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="5f0d1-123">Tworzy publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="5f0d1-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="5f0d1-124">Nowe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="5f0d1-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="5f0d1-125">Tworzy konfiguracji reguły grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="5f0d1-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="5f0d1-126">Ta konfiguracja jest używane toocreate reguły NSG, po utworzeniu hello NSG.</span><span class="sxs-lookup"><span data-stu-id="5f0d1-126">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="5f0d1-127">Nowe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="5f0d1-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="5f0d1-128">Tworzy sieciową grupę zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="5f0d1-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="5f0d1-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5f0d1-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5f0d1-130">Pobiera informacje o podsieci.</span><span class="sxs-lookup"><span data-stu-id="5f0d1-130">Gets subnet information.</span></span> <span data-ttu-id="5f0d1-131">Te informacje jest używany podczas tworzenia interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="5f0d1-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="5f0d1-132">Nowe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="5f0d1-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="5f0d1-133">Tworzy interfejs sieciowy.</span><span class="sxs-lookup"><span data-stu-id="5f0d1-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="5f0d1-134">Nowe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="5f0d1-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="5f0d1-135">Tworzy konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5f0d1-135">Creates a VM configuration.</span></span> <span data-ttu-id="5f0d1-136">Ta konfiguracja zawiera informacje, takie jak nazwa maszyny Wirtualnej, system operacyjny i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="5f0d1-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="5f0d1-137">Konfiguracja Hello jest używany podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5f0d1-137">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="5f0d1-138">Nowe AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="5f0d1-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="5f0d1-139">Utwórz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="5f0d1-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="5f0d1-140">Zestaw AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="5f0d1-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="5f0d1-141">Dodaj maszynę wirtualną toohello rozszerzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5f0d1-141">Add a VM extension toohello virtual machine.</span></span> <span data-ttu-id="5f0d1-142">W takim przypadku hello rozszerzenia agenta Operations Management Suite jest agent pakietu OMS hello tooinstall używane i zarejestrować hello maszyny Wirtualnej w obszarze roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="5f0d1-142">In this case, hello Operations Management Suite agent extension is used tooinstall hello OMS agent and enroll hello VM in an OMS workspace.</span></span> |
|[<span data-ttu-id="5f0d1-143">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5f0d1-143">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="5f0d1-144">Usuwa grupę zasobów i wszystkie zasoby zawarte w ciągu.</span><span class="sxs-lookup"><span data-stu-id="5f0d1-144">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5f0d1-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5f0d1-145">Next steps</span></span>

<span data-ttu-id="5f0d1-146">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5f0d1-146">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5f0d1-147">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5f0d1-147">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
