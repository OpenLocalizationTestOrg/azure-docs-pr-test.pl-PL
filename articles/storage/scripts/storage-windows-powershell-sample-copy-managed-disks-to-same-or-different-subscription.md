---
title: "Przykładowy skrypt programu PowerShell Azure - dyskach do tych samych lub różnych subskrypcji zarządzanych kopiowania (przenoszenia) | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure - kopiowania (przenoszenia) zarządzanych dysków do tych samych lub różnych subskrypcji."
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/06/2017
ms.author: ramankum
ms.openlocfilehash: 6fa94de0461cc538a60d57ca3518141afd9d0469
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="copy-managed-disks-in-the-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="d17ab-103">Kopiowanie dysków zarządzanych w tej samej subskrypcji lub różnych subskrypcji przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="d17ab-103">Copy managed disks in the same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="d17ab-104">Ten skrypt tworzy kopię istniejącego dysku zarządzanych w tej samej subskrypcji lub różnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d17ab-104">This script creates a copy of an existing managed disk in the same subscription or different subscription.</span></span> <span data-ttu-id="d17ab-105">Nowy dysk jest tworzony w tym samym regionie co dysków zarządzanych w nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="d17ab-105">The new disk is created in the same region as the parent managed disk.</span></span>   

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d17ab-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="d17ab-106">Sample script</span></span>

<span data-ttu-id="d17ab-107">[!code-powershell[główne](../../../powershell_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "kopiowania zarządzane dysku")]</span><span class="sxs-lookup"><span data-stu-id="d17ab-107">[!code-powershell[main](../../../powershell_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "Copy managed disk")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="d17ab-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="d17ab-108">Script explanation</span></span>

<span data-ttu-id="d17ab-109">Ten skrypt używa następujących poleceń do tworzenia nowych dysków zarządzanych w subskrypcji docelowej przy użyciu identyfikatora dysków zarządzanych w źródłowym.</span><span class="sxs-lookup"><span data-stu-id="d17ab-109">This script uses following commands to create a new managed disk in the target subscription using the Id of the source managed disk.</span></span> <span data-ttu-id="d17ab-110">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="d17ab-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d17ab-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="d17ab-111">Command</span></span> | <span data-ttu-id="d17ab-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d17ab-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d17ab-113">Nowe AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="d17ab-113">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="d17ab-114">Tworzy konfiguracji dysku, który jest używany do tworzenia dysku.</span><span class="sxs-lookup"><span data-stu-id="d17ab-114">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="d17ab-115">Zawiera ona identyfikator dysku nadrzędnego i lokalizacji, która jest taka sama jak lokalizacja dysku nadrzędnego zasobu.</span><span class="sxs-lookup"><span data-stu-id="d17ab-115">It includes the resource Id of the parent disk and location that is same as the location of parent disk.</span></span>  |
| [<span data-ttu-id="d17ab-116">Nowe AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="d17ab-116">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="d17ab-117">Tworzy dysk przy użyciu konfiguracji dysku, nazwa dysku i przekazywane jako parametry nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="d17ab-117">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="d17ab-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d17ab-118">Next steps</span></span>

[<span data-ttu-id="d17ab-119">Utwórz maszynę wirtualną z dyskiem zarządzanym</span><span class="sxs-lookup"><span data-stu-id="d17ab-119">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="d17ab-120">Aby uzyskać więcej informacji dotyczących modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d17ab-120">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d17ab-121">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w [dokumentacji maszyny Wirtualnej systemu Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d17ab-121">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>