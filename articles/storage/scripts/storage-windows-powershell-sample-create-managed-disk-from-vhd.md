---
title: "aaaAzure przykładowy skrypt programu PowerShell — Tworzenie dysku zarządzanego z pliku VHD na koncie magazynu w tym samym lub różnych subskrypcji | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 93157823eb3b8cddba5e0af455d16bff1d42ce00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a><span data-ttu-id="16916-103">Tworzenie dysku zarządzanego z pliku VHD na koncie magazynu w tym samym lub różnych subskrypcji przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="16916-103">Create a managed disk from a VHD file in a storage account in same or different subscription with PowerShell</span></span>

<span data-ttu-id="16916-104">Ten skrypt tworzy dysków zarządzanych z pliku VHD na koncie magazynu w tym samym lub różnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="16916-104">This script creates a managed disk from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="16916-105">Użyj tego skryptu tooimport specjalne (nie uogólniony/Sysprep) wirtualnego dysku twardego toomanaged OS dysku toocreate maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="16916-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD toomanaged OS disk toocreate a virtual machine.</span></span> <span data-ttu-id="16916-106">Należy także użyć go tooimport dysku danych toomanaged dane wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="16916-106">Also, use it tooimport a data VHD toomanaged data disk.</span></span> 

<span data-ttu-id="16916-107">Nie należy tworzyć wiele identycznych dysków zarządzanych z pliku VHD w krótkim czasie.</span><span class="sxs-lookup"><span data-stu-id="16916-107">Don't create multiple identical managed disks from a VHD file in small amount of time.</span></span> <span data-ttu-id="16916-108">toocreate zarządzane dysków z pliku vhd migawki obiektu blob hello pliku wirtualnego dysku twardego zostaje utworzony, a następnie jest używany toocreate zarządzanych dysków.</span><span class="sxs-lookup"><span data-stu-id="16916-108">toocreate managed disks from a vhd file, blob snapshot of hello vhd file is created and then it is used toocreate managed disks.</span></span> <span data-ttu-id="16916-109">W ciągu jednej minuty powodujące błędy tworzenia dysku można utworzyć migawki tylko jeden obiekt blob toothrottling ukończenia.</span><span class="sxs-lookup"><span data-stu-id="16916-109">Only one blob snapshot can be created in a minute that causes disk creation failures due toothrottling.</span></span> <span data-ttu-id="16916-110">tooavoid tego ograniczenia przepustowości, Utwórz [zarządzanych migawki z pliku vhd hello](./../scripts/storage-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) i następnie użyj hello zarządzane toocreate migawki wiele dysków zarządzanych w krótkim czasie.</span><span class="sxs-lookup"><span data-stu-id="16916-110">tooavoid this throttling, create a [managed snapshot from hello vhd file](./../scripts/storage-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) and then use hello managed snapshot toocreate multiple managed disks in short amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="16916-111">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="16916-111">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="16916-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="16916-112">Script explanation</span></span>

<span data-ttu-id="16916-113">Ten skrypt używa następujących poleceń toocreate dysków zarządzanych z dysku VHD w innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="16916-113">This script uses following commands toocreate a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="16916-114">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="16916-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="16916-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="16916-115">Command</span></span> | <span data-ttu-id="16916-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="16916-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="16916-117">Nowe AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="16916-117">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="16916-118">Tworzy konfiguracji dysku, który jest używany do tworzenia dysku.</span><span class="sxs-lookup"><span data-stu-id="16916-118">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="16916-119">Zawiera typ magazynu, lokalizacji, identyfikator hello konta magazynu przechowywania hello nadrzędnego dysku VHD, identyfikator URI dysku VHD hello elementu nadrzędnego dysku VHD zasobu.</span><span class="sxs-lookup"><span data-stu-id="16916-119">It includes storage type, location, resource Id of hello storage account where hello parent VHD is stored, VHD URI of hello parent VHD.</span></span> |
| [<span data-ttu-id="16916-120">Nowe AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="16916-120">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="16916-121">Tworzy dysk przy użyciu konfiguracji dysku, nazwa dysku i przekazywane jako parametry nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="16916-121">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="16916-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="16916-122">Next steps</span></span>

[<span data-ttu-id="16916-123">Utwórz maszynę wirtualną, dołączając dysków zarządzanych jako dysk systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="16916-123">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="16916-124">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="16916-124">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="16916-125">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="16916-125">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
