---
title: "Przykładowy skrypt programu PowerShell - aaaAzure utworzenia migawki z toocreate wirtualnego dysku twardego wiele takich samych dysków zarządzanych w krótkim czasie | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — Tworzenie migawki z toocreate wirtualnego dysku twardego wiele takich samych dysków zarządzanych w krótkim czasie"
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
ms.openlocfilehash: 0a13e399b692f32b3772add39fe5b5c023808c5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-snapshot-from-a-vhd-toocreate-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a><span data-ttu-id="8ad28-103">Utwórz migawkę z toocreate wirtualnego dysku twardego wiele takich samych dysków zarządzanych w krótkim czasie przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ad28-103">Create a snapshot from a VHD toocreate multiple identical managed disks in small amount of time with PowerShell</span></span>

<span data-ttu-id="8ad28-104">Ten skrypt tworzy migawkę z pliku VHD na koncie magazynu w tym samym lub różnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8ad28-104">This script creates a snapshot from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="8ad28-105">Użyj tego skryptu tooimport specjalne migawki tooa wirtualnego dysku twardego (nie uogólniony/Sysprep) i użycia toocreate migawki hello wiele takich samych dysków zarządzanych w krótkim czasie.</span><span class="sxs-lookup"><span data-stu-id="8ad28-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD tooa snapshot and then use hello snapshot toocreate multiple identical managed disks in small amount of time.</span></span> <span data-ttu-id="8ad28-106">Należy także użyć go tooimport tooa migawki wirtualnego dysku twardego danych a następnie toocreate migawki hello wiele dysków zarządzanych w krótkim czasie.</span><span class="sxs-lookup"><span data-stu-id="8ad28-106">Also, use it tooimport a data VHD tooa snapshot and then use hello snapshot toocreate multiple managed disks in small amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="8ad28-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="8ad28-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="8ad28-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="8ad28-108">Script explanation</span></span>

<span data-ttu-id="8ad28-109">Ten skrypt używa następujących poleceń toocreate dysków zarządzanych z dysku VHD w innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8ad28-109">This script uses following commands toocreate a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="8ad28-110">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="8ad28-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="8ad28-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="8ad28-111">Command</span></span> | <span data-ttu-id="8ad28-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="8ad28-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8ad28-113">Nowe AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="8ad28-113">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="8ad28-114">Tworzy konfiguracji dysku, który jest używany do tworzenia dysku.</span><span class="sxs-lookup"><span data-stu-id="8ad28-114">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="8ad28-115">Zawiera typ magazynu, lokalizacji, identyfikator konta magazynu hello przechowywania hello nadrzędnego dysku VHD zasobu i identyfikator URI dysku VHD hello elementu nadrzędnego dysku VHD.</span><span class="sxs-lookup"><span data-stu-id="8ad28-115">It includes storage type, location, resource Id of hello storage account where hello parent VHD is stored, and VHD URI of hello parent VHD.</span></span> |
| [<span data-ttu-id="8ad28-116">Nowe AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="8ad28-116">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="8ad28-117">Tworzy dysk przy użyciu konfiguracji dysku, nazwa dysku i przekazywane jako parametry nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="8ad28-117">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8ad28-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8ad28-118">Next steps</span></span>

[<span data-ttu-id="8ad28-119">Tworzenie dysku zarządzanego z migawki</span><span class="sxs-lookup"><span data-stu-id="8ad28-119">Create a managed disk from snapshot</span></span>](./../../storage/scripts/storage-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[<span data-ttu-id="8ad28-120">Utwórz maszynę wirtualną, dołączając dysków zarządzanych jako dysk systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="8ad28-120">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="8ad28-121">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8ad28-121">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="8ad28-122">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8ad28-122">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
