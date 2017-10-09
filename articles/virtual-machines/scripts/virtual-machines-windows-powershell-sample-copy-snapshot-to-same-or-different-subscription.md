---
title: "Przykładowy skrypt programu PowerShell — migawki kopiowania (przenoszenia) toosame dysków zarządzanych lub innej subskrypcji aaaAzure | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure - migawki kopiowania (przenoszenia) toosame dysków zarządzanych lub innej subskrypcji"
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
ms.openlocfilehash: d7b8a71cc09d1950271f472e89b95bb551323be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="d0d68-103">Kopiowanie migawek dysków zarządzanych w tej samej subskrypcji lub różnych subskrypcji przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0d68-103">Copy snapshot of a managed disk in same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="d0d68-104">Ten skrypt tworzy kopię migawkę w hello tej samej subskrypcji tej samej lub innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d0d68-104">This script creates a copy of a snapshot in hello same same subscription or different subscription.</span></span> <span data-ttu-id="d0d68-105">Użyj tego skryptu toomove subskrypcji toodifferent migawki dla przechowywania danych.</span><span class="sxs-lookup"><span data-stu-id="d0d68-105">Use this script toomove a snapshot toodifferent subscription for data retention.</span></span> <span data-ttu-id="d0d68-106">Zapisywanie migawek w innej subskrypcji Chroń przed przypadkowym usunięciem migawek w ramach subskrypcji głównego.</span><span class="sxs-lookup"><span data-stu-id="d0d68-106">Storing snapshots in different subscription protect you from accidental deletion of snapshots in your main subscription.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d0d68-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="d0d68-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="d0d68-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="d0d68-108">Script explanation</span></span>

<span data-ttu-id="d0d68-109">Ten skrypt używa następujących poleceń toocreate migawki za pomocą subskrypcji docelowej hello hello identyfikator hello źródła migawki.</span><span class="sxs-lookup"><span data-stu-id="d0d68-109">This script uses following commands toocreate a snapshot in hello target subscription using hello Id of hello source snapshot.</span></span> <span data-ttu-id="d0d68-110">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="d0d68-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d0d68-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="d0d68-111">Command</span></span> | <span data-ttu-id="d0d68-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d0d68-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d0d68-113">Nowe AzureRmSnapshotConfig</span><span class="sxs-lookup"><span data-stu-id="d0d68-113">New-AzureRmSnapshotConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | <span data-ttu-id="d0d68-114">Tworzy konfigurację migawki, która służy do tworzenia migawek.</span><span class="sxs-lookup"><span data-stu-id="d0d68-114">Creates snapshot configuration that is used for snapshot creation.</span></span> <span data-ttu-id="d0d68-115">Obejmuje on zasobów hello identyfikator migawki nadrzędnego hello i lokalizacji, która jest taka sama jak hello nadrzędnego migawki.</span><span class="sxs-lookup"><span data-stu-id="d0d68-115">It includes hello resource Id of hello parent snapshot and location that is same as hello parent snapshot.</span></span>  |
| [<span data-ttu-id="d0d68-116">Nowe AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="d0d68-116">New-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="d0d68-117">Tworzy migawkę przy użyciu konfiguracji migawki, nazwę migawki i przekazywane jako parametry nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="d0d68-117">Creates a snapshot using snapshot configuration, snapshot name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="d0d68-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d0d68-118">Next steps</span></span>

[<span data-ttu-id="d0d68-119">Utwórz maszynę wirtualną z migawki</span><span class="sxs-lookup"><span data-stu-id="d0d68-119">Create a virtual machine from a snapshot</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="d0d68-120">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d0d68-120">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d0d68-121">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d0d68-121">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
