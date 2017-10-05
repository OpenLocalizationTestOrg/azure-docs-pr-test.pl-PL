---
title: "Skrypt programu PowerShell Azure przykładowe — Tworzenie migawki z dysku VHD, aby utworzyć wiele takich samych dysków zarządzanych w krótkim czasie | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — Tworzenie migawki z dysku VHD, aby utworzyć wiele takich samych dysków zarządzanych w krótkim czasie"
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
ms.openlocfilehash: 02a69abd6c17ce765996379309e22afad82c4e10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-snapshot-from-a-vhd-to-create-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a><span data-ttu-id="7eee3-103">Utwórz migawkę z dysku VHD, aby utworzyć wiele takich samych dysków zarządzanych w krótkim czasie przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="7eee3-103">Create a snapshot from a VHD to create multiple identical managed disks in small amount of time with PowerShell</span></span>

<span data-ttu-id="7eee3-104">Ten skrypt tworzy migawkę z pliku VHD na koncie magazynu w tym samym lub różnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7eee3-104">This script creates a snapshot from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="7eee3-105">Użyj tego skryptu, aby importować specjalne (nie uogólniony/Sysprep) dysk VHD do migawki i skorzystaj z migawki można tworzyć wiele identycznych dyskach zarządzanych w krótkim czasie.</span><span class="sxs-lookup"><span data-stu-id="7eee3-105">Use this script to import a specialized (not generalized/sysprepped) VHD to a snapshot and then use the snapshot to create multiple identical managed disks in small amount of time.</span></span> <span data-ttu-id="7eee3-106">Ponadto należy zaimportować dane wirtualnego dysku twardego do migawki, a następnie utwórz wiele dysków zarządzanych w krótkim czasie za pomocą migawki.</span><span class="sxs-lookup"><span data-stu-id="7eee3-106">Also, use it to import a data VHD to a snapshot and then use the snapshot to create multiple managed disks in small amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="7eee3-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="7eee3-107">Sample script</span></span>

<span data-ttu-id="7eee3-108">[!code-powershell[główne](../../../powershell_scripts/virtual-machine/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Tworzenie migawki z wirtualnego dysku twardego")]</span><span class="sxs-lookup"><span data-stu-id="7eee3-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="7eee3-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="7eee3-109">Script explanation</span></span>

<span data-ttu-id="7eee3-110">Ten skrypt używa następujących poleceń w celu utworzenia dysków zarządzanych z dysku VHD w innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7eee3-110">This script uses following commands to create a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="7eee3-111">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="7eee3-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="7eee3-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="7eee3-112">Command</span></span> | <span data-ttu-id="7eee3-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="7eee3-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7eee3-114">Nowe AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="7eee3-114">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="7eee3-115">Tworzy konfiguracji dysku, który jest używany do tworzenia dysku.</span><span class="sxs-lookup"><span data-stu-id="7eee3-115">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="7eee3-116">Zawiera typ magazynu, lokalizacji, identyfikator konta magazynu, w którym przechowywana jest nadrzędny dysk VHD zasobu i identyfikator URI dysku VHD elementu nadrzędnego dysku VHD.</span><span class="sxs-lookup"><span data-stu-id="7eee3-116">It includes storage type, location, resource Id of the storage account where the parent VHD is stored, and VHD URI of the parent VHD.</span></span> |
| [<span data-ttu-id="7eee3-117">Nowe AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="7eee3-117">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="7eee3-118">Tworzy dysk przy użyciu konfiguracji dysku, nazwa dysku i przekazywane jako parametry nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="7eee3-118">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7eee3-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7eee3-119">Next steps</span></span>

[<span data-ttu-id="7eee3-120">Tworzenie dysku zarządzanego z migawki</span><span class="sxs-lookup"><span data-stu-id="7eee3-120">Create a managed disk from snapshot</span></span>](virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[<span data-ttu-id="7eee3-121">Utwórz maszynę wirtualną, dołączając dysków zarządzanych jako dysk systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="7eee3-121">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="7eee3-122">Aby uzyskać więcej informacji dotyczących modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7eee3-122">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="7eee3-123">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w [dokumentacji maszyny Wirtualnej systemu Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7eee3-123">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>