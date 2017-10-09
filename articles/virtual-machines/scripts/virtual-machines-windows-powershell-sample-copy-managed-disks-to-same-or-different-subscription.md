---
title: "Przykładowy skrypt programu PowerShell - aaaAzure kopiowania (przenoszenia) zarządzane toosame dysków lub innej subskrypcji | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure — toosame dysków zarządzanych kopiowania (przenoszenia) lub innej subskrypcji"
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
ms.openlocfilehash: 22e19a47228cbf628bebebd73012b8aa7baf073c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-in-hello-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="d753c-103">Kopiuj zarządzane dyski w hello takie same subskrypcji lub różnych subskrypcji przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="d753c-103">Copy managed disks in hello same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="d753c-104">Ten skrypt tworzy kopię istniejącego dysku zarządzanego w hello tej samej subskrypcji lub różnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d753c-104">This script creates a copy of an existing managed disk in hello same subscription or different subscription.</span></span> <span data-ttu-id="d753c-105">Witaj nowy dysk jest tworzony w hello sam region jako element nadrzędny hello zarządzane dysku.</span><span class="sxs-lookup"><span data-stu-id="d753c-105">hello new disk is created in hello same region as hello parent managed disk.</span></span>   

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d753c-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="d753c-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "Copy managed disk")]


## <a name="script-explanation"></a><span data-ttu-id="d753c-107">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="d753c-107">Script explanation</span></span>

<span data-ttu-id="d753c-108">Ten skrypt używa następujących poleceń toocreate nowy dysk zarządzanych za pomocą subskrypcji docelowej hello hello identyfikator źródła hello zarządzane dysku.</span><span class="sxs-lookup"><span data-stu-id="d753c-108">This script uses following commands toocreate a new managed disk in hello target subscription using hello Id of hello source managed disk.</span></span> <span data-ttu-id="d753c-109">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="d753c-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d753c-110">Polecenie</span><span class="sxs-lookup"><span data-stu-id="d753c-110">Command</span></span> | <span data-ttu-id="d753c-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d753c-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d753c-112">Nowe AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="d753c-112">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="d753c-113">Tworzy konfiguracji dysku, który jest używany do tworzenia dysku.</span><span class="sxs-lookup"><span data-stu-id="d753c-113">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="d753c-114">Obejmuje on zasobów hello identyfikator dysku nadrzędnego hello i lokalizacji, która jest taka sama jak lokalizacja hello dysku nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="d753c-114">It includes hello resource Id of hello parent disk and location that is same as hello location of parent disk.</span></span>  |
| [<span data-ttu-id="d753c-115">Nowe AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="d753c-115">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="d753c-116">Tworzy dysk przy użyciu konfiguracji dysku, nazwa dysku i przekazywane jako parametry nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="d753c-116">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="d753c-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d753c-117">Next steps</span></span>

[<span data-ttu-id="d753c-118">Utwórz maszynę wirtualną z dyskiem zarządzanym</span><span class="sxs-lookup"><span data-stu-id="d753c-118">Create a virtual machine from a managed disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="d753c-119">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d753c-119">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d753c-120">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d753c-120">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
