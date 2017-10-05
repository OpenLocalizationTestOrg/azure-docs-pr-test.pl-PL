---
title: "Skrypt programu PowerShell Azure przykładowe — tworzenie dysków zarządzanych z pliku VHD na koncie magazynu w tym samym lub różnych subskrypcji | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — tworzenie dysków zarządzanych z pliku VHD na koncie magazynu w tym samym lub różnych subskrypcji."
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
ms.openlocfilehash: 728def40a3eb132537decbd099fa71f4544c6b87
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a><span data-ttu-id="a9b6d-103">Tworzenie dysku zarządzanego z pliku VHD na koncie magazynu w tym samym lub różnych subskrypcji przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9b6d-103">Create a managed disk from a VHD file in a storage account in same or different subscription with PowerShell</span></span>

<span data-ttu-id="a9b6d-104">Ten skrypt tworzy dysków zarządzanych z pliku VHD na koncie magazynu w tym samym lub różnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-104">This script creates a managed disk from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="a9b6d-105">Użyj tego skryptu, aby importować specjalne (nie uogólniony/Sysprep) wirtualnego dysku twardego na dysku systemu operacyjnego zarządzanych do utworzenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-105">Use this script to import a specialized (not generalized/sysprepped) VHD to managed OS disk to create a virtual machine.</span></span> <span data-ttu-id="a9b6d-106">Należy także użyć go do importowania danych dysku VHD na dysk danych zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-106">Also, use it to import a data VHD to managed data disk.</span></span> 

<span data-ttu-id="a9b6d-107">Nie należy tworzyć wiele identycznych dysków zarządzanych z pliku VHD w krótkim czasie.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-107">Don't create multiple identical managed disks from a VHD file in small amount of time.</span></span> <span data-ttu-id="a9b6d-108">Do tworzenia zarządzanego dysków z pliku vhd, obiektów blob migawki pliku vhd jest tworzony i następnie jest używany do tworzenia dysków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-108">To create managed disks from a vhd file, blob snapshot of the vhd file is created and then it is used to create managed disks.</span></span> <span data-ttu-id="a9b6d-109">W ciągu jednej minuty powodujące błędy tworzenia dysku z powodu dławienia można utworzyć migawki tylko jeden obiekt blob.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-109">Only one blob snapshot can be created in a minute that causes disk creation failures due to throttling.</span></span> <span data-ttu-id="a9b6d-110">Aby uniknąć tego ograniczenia przepustowości, Utwórz [zarządzanych migawki z pliku vhd](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) i następnie użyj zarządzanego migawki, aby utworzyć wiele zarządzanych w skrócie dyski ilość czasu.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-110">To avoid this throttling, create a [managed snapshot from the vhd file](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) and then use the managed snapshot to create multiple managed disks in short amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a9b6d-111">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="a9b6d-111">Sample script</span></span>

<span data-ttu-id="a9b6d-112">[!code-powershell[główne](../../../powershell_scripts/virtual-machine/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "tworzenie dysków zarządzanych z wirtualnego dysku twardego")]</span><span class="sxs-lookup"><span data-stu-id="a9b6d-112">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="a9b6d-113">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="a9b6d-113">Script explanation</span></span>

<span data-ttu-id="a9b6d-114">Ten skrypt używa następujących poleceń w celu utworzenia dysków zarządzanych z dysku VHD w innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-114">This script uses following commands to create a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="a9b6d-115">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a9b6d-116">Polecenie</span><span class="sxs-lookup"><span data-stu-id="a9b6d-116">Command</span></span> | <span data-ttu-id="a9b6d-117">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a9b6d-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a9b6d-118">Nowe AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="a9b6d-118">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="a9b6d-119">Tworzy konfiguracji dysku, który jest używany do tworzenia dysku.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-119">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="a9b6d-120">Zawiera typ magazynu, lokalizacji, identyfikator konto magazynu, w którym przechowywane nadrzędnego dysku VHD, identyfikator URI dysku VHD elementu nadrzędnego dysku VHD zasobu.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-120">It includes storage type, location, resource Id of the storage account where the parent VHD is stored, VHD URI of the parent VHD.</span></span> |
| [<span data-ttu-id="a9b6d-121">Nowe AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="a9b6d-121">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="a9b6d-122">Tworzy dysk przy użyciu konfiguracji dysku, nazwa dysku i przekazywane jako parametry nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="a9b6d-122">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a9b6d-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a9b6d-123">Next steps</span></span>

[<span data-ttu-id="a9b6d-124">Utwórz maszynę wirtualną, dołączając dysków zarządzanych jako dysk systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="a9b6d-124">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="a9b6d-125">Aby uzyskać więcej informacji dotyczących modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a9b6d-125">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a9b6d-126">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w [dokumentacji maszyny Wirtualnej systemu Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a9b6d-126">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>