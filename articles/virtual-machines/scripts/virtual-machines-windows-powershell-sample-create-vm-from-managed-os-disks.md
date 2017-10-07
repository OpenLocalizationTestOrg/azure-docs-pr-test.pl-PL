---
title: "aaaAzure przykładowy skrypt programu PowerShell — Utwórz maszynę Wirtualną, dołączając dysków zarządzanych jako dysk systemu operacyjnego | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — Utwórz maszynę Wirtualną, dołączając dysków zarządzanych jako dysk systemu operacyjnego"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 8ae5b14df3977a4af91b92692cb925199cfb8058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-powershell"></a><span data-ttu-id="e76c8-103">Utwórz maszynę wirtualną przy użyciu istniejącego dysku systemu operacyjnego zarządzane przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="e76c8-103">Create a virtual machine using an existing managed OS disk with PowerShell</span></span>

<span data-ttu-id="e76c8-104">Ten skrypt tworzy maszynę wirtualną, dołączając istniejący dysk zarządzane jako dysk systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="e76c8-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="e76c8-105">Użyj tego skryptu w poprzednich scenariuszach:</span><span class="sxs-lookup"><span data-stu-id="e76c8-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="e76c8-106">Tworzenie maszyny Wirtualnej z istniejącego zarządzanych dysk systemu operacyjnego, który został skopiowany z dysków zarządzanych w innej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e76c8-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="e76c8-107">Tworzenie maszyny Wirtualnej z istniejącego dysku zarządzanego utworzony na podstawie specjalne pliku wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="e76c8-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="e76c8-108">Tworzenie maszyny Wirtualnej z istniejącego zarządzanych dysk systemu operacyjnego, który został utworzony na podstawie migawki</span><span class="sxs-lookup"><span data-stu-id="e76c8-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e76c8-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="e76c8-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from snapshot")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e76c8-110">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="e76c8-110">Clean up deployment</span></span> 

<span data-ttu-id="e76c8-111">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="e76c8-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="e76c8-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="e76c8-112">Script explanation</span></span>

<span data-ttu-id="e76c8-113">Ten skrypt używa hello następujące właściwości dysku tooget zarządzane poleceń, Dołącz tooa dysków zarządzanych w nowej maszyny Wirtualnej i tworzenie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e76c8-113">This script uses hello following commands tooget managed disk properties, attach a managed disk tooa new VM and create a VM.</span></span> <span data-ttu-id="e76c8-114">Każdy element w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="e76c8-114">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e76c8-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="e76c8-115">Command</span></span> | <span data-ttu-id="e76c8-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="e76c8-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e76c8-117">Get-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="e76c8-117">Get-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Get-AzureRmDisk) | <span data-ttu-id="e76c8-118">Pobiera obiekt na podstawie nazwy hello i grupy zasobów hello dysku.</span><span class="sxs-lookup"><span data-stu-id="e76c8-118">Gets disk object based on hello name and hello resource group of a disk.</span></span> <span data-ttu-id="e76c8-119">Identyfikator właściwości hello zwrócony obiekt tooa dysku hello tooattach używane nowej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e76c8-119">Id property of hello returned disk object is used tooattach hello disk tooa new VM</span></span> |
| [<span data-ttu-id="e76c8-120">Nowe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="e76c8-120">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="e76c8-121">Tworzy konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e76c8-121">Creates a VM configuration.</span></span> <span data-ttu-id="e76c8-122">Ta konfiguracja zawiera informacje, takie jak nazwa maszyny Wirtualnej, system operacyjny i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="e76c8-122">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="e76c8-123">Konfiguracja Hello jest używany podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e76c8-123">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="e76c8-124">Zestaw AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="e76c8-124">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="e76c8-125">Dołącza dysk zarządzane przy użyciu właściwości identyfikatora hello hello dysku jako systemu operacyjnego dysku tooa nowej maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e76c8-125">Attaches a managed disk using hello Id property of hello disk as OS disk tooa new virtual machine</span></span> |
| [<span data-ttu-id="e76c8-126">Nowe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="e76c8-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="e76c8-127">Tworzy publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="e76c8-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="e76c8-128">Nowe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="e76c8-128">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="e76c8-129">Tworzy interfejs sieciowy.</span><span class="sxs-lookup"><span data-stu-id="e76c8-129">Creates a network interface.</span></span> |
| [<span data-ttu-id="e76c8-130">Nowe AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="e76c8-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="e76c8-131">Utwórz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="e76c8-131">Create a virtual machine.</span></span> |
|[<span data-ttu-id="e76c8-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e76c8-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="e76c8-133">Usuwa grupę zasobów i wszystkie zasoby zawarte w ciągu.</span><span class="sxs-lookup"><span data-stu-id="e76c8-133">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e76c8-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e76c8-134">Next steps</span></span>

<span data-ttu-id="e76c8-135">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e76c8-135">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e76c8-136">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e76c8-136">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
