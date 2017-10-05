---
title: "Przykładowy skrypt programu PowerShell Azure - migawki kopiowania (przenoszenia) dysków zarządzanych do tych samych lub różnych subskrypcji | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure - migawki kopiowania (przenoszenia) dysków zarządzanych do tych samych lub różnych subskrypcji"
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
ms.openlocfilehash: 69b9b4ed86117f7fe561e7e70227e60e6a9d858e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="c6c78-103">Kopiowanie migawek dysków zarządzanych w tej samej subskrypcji lub różnych subskrypcji przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6c78-103">Copy snapshot of a managed disk in same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="c6c78-104">Ten skrypt tworzy kopię migawkę w tej samej subskrypcji tej samej lub innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c6c78-104">This script creates a copy of a snapshot in the same same subscription or different subscription.</span></span> <span data-ttu-id="c6c78-105">Użyj tego skryptu można przenieść do innej subskrypcji dla przechowywania danych migawki.</span><span class="sxs-lookup"><span data-stu-id="c6c78-105">Use this script to move a snapshot to different subscription for data retention.</span></span> <span data-ttu-id="c6c78-106">Zapisywanie migawek w innej subskrypcji Chroń przed przypadkowym usunięciem migawek w ramach subskrypcji głównego.</span><span class="sxs-lookup"><span data-stu-id="c6c78-106">Storing snapshots in different subscription protect you from accidental deletion of snapshots in your main subscription.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c6c78-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="c6c78-107">Sample script</span></span>

<span data-ttu-id="c6c78-108">[!code-powershell[główne](../../../powershell_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "migawki kopiowania")]</span><span class="sxs-lookup"><span data-stu-id="c6c78-108">[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="c6c78-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="c6c78-109">Script explanation</span></span>

<span data-ttu-id="c6c78-110">Ten skrypt używa następujących poleceń do tworzenia migawek w subskrypcji docelowej przy użyciu identyfikatora migawki źródła.</span><span class="sxs-lookup"><span data-stu-id="c6c78-110">This script uses following commands to create a snapshot in the target subscription using the Id of the source snapshot.</span></span> <span data-ttu-id="c6c78-111">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="c6c78-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c6c78-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="c6c78-112">Command</span></span> | <span data-ttu-id="c6c78-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c6c78-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c6c78-114">Nowe AzureRmSnapshotConfig</span><span class="sxs-lookup"><span data-stu-id="c6c78-114">New-AzureRmSnapshotConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | <span data-ttu-id="c6c78-115">Tworzy konfigurację migawki, która służy do tworzenia migawek.</span><span class="sxs-lookup"><span data-stu-id="c6c78-115">Creates snapshot configuration that is used for snapshot creation.</span></span> <span data-ttu-id="c6c78-116">Zawiera ona identyfikator nadrzędnego migawki i lokalizacji, która jest taka sama jak nadrzędnego migawki zasobu.</span><span class="sxs-lookup"><span data-stu-id="c6c78-116">It includes the resource Id of the parent snapshot and location that is same as the parent snapshot.</span></span>  |
| [<span data-ttu-id="c6c78-117">Nowe AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="c6c78-117">New-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="c6c78-118">Tworzy migawkę przy użyciu konfiguracji migawki, nazwę migawki i przekazywane jako parametry nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="c6c78-118">Creates a snapshot using snapshot configuration, snapshot name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="c6c78-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c6c78-119">Next steps</span></span>

[<span data-ttu-id="c6c78-120">Utwórz maszynę wirtualną z migawki</span><span class="sxs-lookup"><span data-stu-id="c6c78-120">Create a virtual machine from a snapshot</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="c6c78-121">Aby uzyskać więcej informacji dotyczących modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c6c78-121">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c6c78-122">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w [dokumentacji maszyny Wirtualnej systemu Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c6c78-122">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>