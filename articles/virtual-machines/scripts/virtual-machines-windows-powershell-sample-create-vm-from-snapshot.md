---
title: "aaaAzure przykładowy skrypt programu PowerShell — tworzenie maszyny Wirtualnej z migawki | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — tworzenie maszyny Wirtualnej z migawki"
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
ms.openlocfilehash: 89c65171b55bff0582c4a26df0b0f29f556845fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-powershell"></a><span data-ttu-id="f279f-103">Utwórz maszynę wirtualną z migawki przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="f279f-103">Create a virtual machine from a snapshot with PowerShell</span></span>

<span data-ttu-id="f279f-104">Ten skrypt tworzy maszynę wirtualną z migawki dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="f279f-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f279f-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="f279f-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from managed os disk")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f279f-106">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="f279f-106">Clean up deployment</span></span> 

<span data-ttu-id="f279f-107">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="f279f-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f279f-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="f279f-108">Script explanation</span></span>

<span data-ttu-id="f279f-109">Ten skrypt używa hello następujące polecenia właściwości migawki tooget, tworzenie dysku zarządzanego z migawki i tworzenie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f279f-109">This script uses hello following commands tooget snapshot properties, create a managed disk from snapshot and create a VM.</span></span> <span data-ttu-id="f279f-110">Każdy element w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="f279f-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f279f-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="f279f-111">Command</span></span> | <span data-ttu-id="f279f-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="f279f-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f279f-113">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="f279f-113">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/get-azurermsnapshot) | <span data-ttu-id="f279f-114">Pobiera migawkę przy użyciu nazwy migawki.</span><span class="sxs-lookup"><span data-stu-id="f279f-114">Gets a snapshot using snapshot name.</span></span> |
| [<span data-ttu-id="f279f-115">Nowe AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="f279f-115">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/new-azurermdiskconfig) | <span data-ttu-id="f279f-116">Tworzy konfiguracji dysku.</span><span class="sxs-lookup"><span data-stu-id="f279f-116">Creates a disk configuration.</span></span> <span data-ttu-id="f279f-117">Ta konfiguracja jest używana z procesu tworzenia dysku hello.</span><span class="sxs-lookup"><span data-stu-id="f279f-117">This configuration is used with hello disk creation process.</span></span> |
| [<span data-ttu-id="f279f-118">Nowe AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="f279f-118">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/new-azurermdisk) | <span data-ttu-id="f279f-119">Tworzy dysków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="f279f-119">Creates a managed disk.</span></span> |
| [<span data-ttu-id="f279f-120">Nowe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="f279f-120">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="f279f-121">Tworzy konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f279f-121">Creates a VM configuration.</span></span> <span data-ttu-id="f279f-122">Ta konfiguracja zawiera informacje, takie jak nazwa maszyny Wirtualnej, system operacyjny i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="f279f-122">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="f279f-123">Konfiguracja Hello jest używany podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f279f-123">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="f279f-124">Zestaw AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="f279f-124">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="f279f-125">Dołącza hello dysków zarządzanych jako maszyna wirtualna toohello dysku systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="f279f-125">Attaches hello managed disk as OS disk toohello virtual machine</span></span> |
| [<span data-ttu-id="f279f-126">Nowe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="f279f-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="f279f-127">Tworzy publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="f279f-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="f279f-128">Nowe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="f279f-128">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="f279f-129">Tworzy interfejs sieciowy.</span><span class="sxs-lookup"><span data-stu-id="f279f-129">Creates a network interface.</span></span> |
| [<span data-ttu-id="f279f-130">Nowe AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="f279f-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="f279f-131">Tworzy maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="f279f-131">Creates a virtual machine.</span></span> |
|[<span data-ttu-id="f279f-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f279f-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="f279f-133">Usuwa grupę zasobów i wszystkie zasoby zawarte w ciągu.</span><span class="sxs-lookup"><span data-stu-id="f279f-133">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f279f-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f279f-134">Next steps</span></span>

<span data-ttu-id="f279f-135">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f279f-135">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f279f-136">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f279f-136">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
