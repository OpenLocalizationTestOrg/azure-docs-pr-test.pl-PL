---
title: "aaaAzure przykładowy skrypt programu PowerShell — Tworzenie dysku zarządzanego z migawki | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — tworzenie dysków zarządzanych z migawki"
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
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: 4fa34a8d6c67171083fba9a9ad73ecca5e0f0229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-powershell"></a><span data-ttu-id="f9d2a-103">Tworzenie dysku zarządzanego z migawki przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9d2a-103">Create a managed disk from a snapshot with PowerShell</span></span>

<span data-ttu-id="f9d2a-104">Ten skrypt tworzy dysków zarządzanych z migawki.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="f9d2a-105">Użyj toorestore maszynę wirtualną z migawek systemu operacyjnego i dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-105">Use it toorestore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="f9d2a-106">Utwórz systemu operacyjnego i danych zarządzanych dysków z odpowiednich migawki, a następnie utwórz nową maszynę wirtualną dołączając dysków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="f9d2a-107">Można także przywrócić dysków z danymi z istniejącej maszyny Wirtualnej, dołączając dyski danych utworzone na podstawie migawki.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f9d2a-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="f9d2a-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Create managed disk from snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="f9d2a-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="f9d2a-109">Script explanation</span></span>

<span data-ttu-id="f9d2a-110">Ten skrypt używa następujących poleceń toocreate dysków zarządzanych z migawki.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-110">This script uses following commands toocreate a managed disk from a snapshot.</span></span> <span data-ttu-id="f9d2a-111">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f9d2a-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="f9d2a-112">Command</span></span> | <span data-ttu-id="f9d2a-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="f9d2a-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f9d2a-114">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="f9d2a-114">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/Get-AzureRmSnapshot) | <span data-ttu-id="f9d2a-115">Pobiera właściwości migawki.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-115">Gets snapshot properties.</span></span>  |
| [<span data-ttu-id="f9d2a-116">Nowe AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="f9d2a-116">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="f9d2a-117">Tworzy konfiguracji dysku, który jest używany do tworzenia dysku.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-117">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="f9d2a-118">Obejmuje on zasobów hello identyfikator hello nadrzędnego migawki, lokalizacji, która jest taka sama jak lokalizacja hello nadrzędnego migawki i hello typu magazynu.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-118">It includes hello resource Id of hello parent snapshot, location that is same as hello location of parent snapshot and hello storage type.</span></span>  |
| [<span data-ttu-id="f9d2a-119">Nowe AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="f9d2a-119">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="f9d2a-120">Tworzy dysk przy użyciu konfiguracji dysku, nazwa dysku i przekazywane jako parametry nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-120">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="f9d2a-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f9d2a-121">Next steps</span></span>

[<span data-ttu-id="f9d2a-122">Utwórz maszynę wirtualną z dyskiem zarządzanym</span><span class="sxs-lookup"><span data-stu-id="f9d2a-122">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="f9d2a-123">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f9d2a-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f9d2a-124">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f9d2a-124">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
