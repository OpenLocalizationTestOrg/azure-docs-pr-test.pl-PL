---
title: "aaaAzure przykładowym skrypcie programu PowerShell - migawki eksportu/kopiowania co konto magazynu tooa wirtualnego dysku twardego w innym regionie | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure - migawki eksportu/kopiowania co konto magazynu tooa wirtualnego dysku twardego w tym samym regionie innym"
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
ms.openlocfilehash: c18ad4fa0bf12033fafe941a807e7b4c8d233a30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-powershell"></a><span data-ttu-id="ad1b8-103">Eksport/kopiowania zarządzane migawki co konto magazynu tooa wirtualnego dysku twardego w innym regionie przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad1b8-103">Export/Copy managed snapshots as VHD tooa storage account in different region with PowerShell</span></span>

<span data-ttu-id="ad1b8-104">Ten skrypt eksportuje migawki zarządzanego konta magazynu tooa w innym regionie.</span><span class="sxs-lookup"><span data-stu-id="ad1b8-104">This script exports a managed snapshot tooa storage account in different region.</span></span> <span data-ttu-id="ad1b8-105">Najpierw generuje hello identyfikatora URI połączenia SAS hello migawki, a następnie używa go po toocopy go tooa konta magazynu w innym regionie.</span><span class="sxs-lookup"><span data-stu-id="ad1b8-105">It first generates hello SAS URI of hello snapshot and then uses it toocopy it tooa storage account in different region.</span></span> <span data-ttu-id="ad1b8-106">Użyj tej kopii zapasowej toomaintain skryptu dysków zarządzanych w innym regionie odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="ad1b8-106">Use this script toomaintain backup of your managed disks in different region for disaster recovery.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ad1b8-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="ad1b8-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="ad1b8-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="ad1b8-108">Script explanation</span></span>

<span data-ttu-id="ad1b8-109">Ten skrypt używa następujących poleceń toogenerate identyfikator URI sygnatury dostępu Współdzielonego dla zarządzanych hello migawki i kopii migawki tooa konto magazynu przy użyciu identyfikatora URI połączenia SAS.</span><span class="sxs-lookup"><span data-stu-id="ad1b8-109">This script uses following commands toogenerate SAS URI for a managed snapshot and copies hello snapshot tooa storage account using SAS URI.</span></span> <span data-ttu-id="ad1b8-110">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="ad1b8-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ad1b8-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="ad1b8-111">Command</span></span> | <span data-ttu-id="ad1b8-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="ad1b8-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ad1b8-113">Udziel AzureRmSnapshotAccess</span><span class="sxs-lookup"><span data-stu-id="ad1b8-113">Grant-AzureRmSnapshotAccess</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="ad1b8-114">Generuje identyfikator URI sygnatury dostępu Współdzielonego dla migawki, która jest używana toocopy on tooa konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="ad1b8-114">Generates SAS URI for a snapshot that is used toocopy it tooa storage account.</span></span> |
| [<span data-ttu-id="ad1b8-115">Nowe AzureStorageContext</span><span class="sxs-lookup"><span data-stu-id="ad1b8-115">New-AzureStorageContext</span></span>](/powershell/module/azure.storage/New-AzureStorageContext) | <span data-ttu-id="ad1b8-116">Tworzy kontekst konta magazynu przy użyciu hello nazwę konta i klucz.</span><span class="sxs-lookup"><span data-stu-id="ad1b8-116">Creates a storage account context using hello account name and key.</span></span> <span data-ttu-id="ad1b8-117">Tego kontekstu może być używane tooperform operacji odczytu/zapisu na powitania konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="ad1b8-117">This context can be used tooperform read/write operations on hello storage account.</span></span> |
| [<span data-ttu-id="ad1b8-118">Start AzureStorageBlobCopy</span><span class="sxs-lookup"><span data-stu-id="ad1b8-118">Start-AzureStorageBlobCopy</span></span>](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | <span data-ttu-id="ad1b8-119">Kopie hello podstawowy dysk VHD konta magazynu tooa migawki</span><span class="sxs-lookup"><span data-stu-id="ad1b8-119">Copies hello underlying VHD of a snapshot tooa storage account</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ad1b8-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ad1b8-120">Next steps</span></span>

[<span data-ttu-id="ad1b8-121">Tworzenie dysku zarządzanego z wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="ad1b8-121">Create a managed disk from a VHD</span></span>](virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[<span data-ttu-id="ad1b8-122">Utwórz maszynę wirtualną z dyskiem zarządzanym</span><span class="sxs-lookup"><span data-stu-id="ad1b8-122">Create a virtual machine from a managed disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="ad1b8-123">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ad1b8-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ad1b8-124">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ad1b8-124">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
