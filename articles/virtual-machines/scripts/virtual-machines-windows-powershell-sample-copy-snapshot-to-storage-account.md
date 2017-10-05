---
title: "Przykładowy skrypt programu PowerShell Azure - migawki eksportu/kopiowania jako dysk VHD do konta magazynu w innym regionie | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure - migawki eksportu/kopiowania jako dysk VHD do konta magazynu w tym samym regionie innym"
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
ms.openlocfilehash: a6bd0686842282ccd7ce0c31bb0152beb30bea66
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-to-a-storage-account-in-different-region-with-powershell"></a><span data-ttu-id="29ce1-103">Eksport/kopiowania zarządzane migawki jako dysk VHD do konta magazynu w innym regionie przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="29ce1-103">Export/Copy managed snapshots as VHD to a storage account in different region with PowerShell</span></span>

<span data-ttu-id="29ce1-104">Ten skrypt eksportuje zarządzanych migawki na konto magazynu w innym regionie.</span><span class="sxs-lookup"><span data-stu-id="29ce1-104">This script exports a managed snapshot to a storage account in different region.</span></span> <span data-ttu-id="29ce1-105">Najpierw generuje identyfikator URI sygnatury dostępu Współdzielonego migawki, a następnie używa, aby skopiować go do konta magazynu w innym regionie.</span><span class="sxs-lookup"><span data-stu-id="29ce1-105">It first generates the SAS URI of the snapshot and then uses it to copy it to a storage account in different region.</span></span> <span data-ttu-id="29ce1-106">Użyj tego skryptu do obsługi kopii zapasowych dysków zarządzanych w innym regionie odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="29ce1-106">Use this script to maintain backup of your managed disks in different region for disaster recovery.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="29ce1-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="29ce1-107">Sample script</span></span>

<span data-ttu-id="29ce1-108">[!code-powershell[główne](../../../powershell_scripts/virtual-machine/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "migawki kopiowania")]</span><span class="sxs-lookup"><span data-stu-id="29ce1-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="29ce1-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="29ce1-109">Script explanation</span></span>

<span data-ttu-id="29ce1-110">Ten skrypt używa następujących poleceń, można wygenerować identyfikatora URI sygnatury dostępu Współdzielonego dla zarządzanych migawki i kopiuje migawki na konto magazynu przy użyciu identyfikatora URI połączenia SAS.</span><span class="sxs-lookup"><span data-stu-id="29ce1-110">This script uses following commands to generate SAS URI for a managed snapshot and copies the snapshot to a storage account using SAS URI.</span></span> <span data-ttu-id="29ce1-111">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="29ce1-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="29ce1-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="29ce1-112">Command</span></span> | <span data-ttu-id="29ce1-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="29ce1-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="29ce1-114">Udziel AzureRmSnapshotAccess</span><span class="sxs-lookup"><span data-stu-id="29ce1-114">Grant-AzureRmSnapshotAccess</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="29ce1-115">Generuje identyfikator URI sygnatury dostępu Współdzielonego dla migawki, która jest używana, aby skopiować go do konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="29ce1-115">Generates SAS URI for a snapshot that is used to copy it to a storage account.</span></span> |
| [<span data-ttu-id="29ce1-116">Nowe AzureStorageContext</span><span class="sxs-lookup"><span data-stu-id="29ce1-116">New-AzureStorageContext</span></span>](/powershell/module/azure.storage/New-AzureStorageContext) | <span data-ttu-id="29ce1-117">Tworzy kontekst konta magazynu przy użyciu nazwy konta i klucz.</span><span class="sxs-lookup"><span data-stu-id="29ce1-117">Creates a storage account context using the account name and key.</span></span> <span data-ttu-id="29ce1-118">Tego kontekstu może służyć do wykonywania operacji odczytu/zapisu na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="29ce1-118">This context can be used to perform read/write operations on the storage account.</span></span> |
| [<span data-ttu-id="29ce1-119">Start AzureStorageBlobCopy</span><span class="sxs-lookup"><span data-stu-id="29ce1-119">Start-AzureStorageBlobCopy</span></span>](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | <span data-ttu-id="29ce1-120">Kopiuje podstawowy dysk VHD migawki na konto magazynu</span><span class="sxs-lookup"><span data-stu-id="29ce1-120">Copies the underlying VHD of a snapshot to a storage account</span></span> |

## <a name="next-steps"></a><span data-ttu-id="29ce1-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="29ce1-121">Next steps</span></span>

[<span data-ttu-id="29ce1-122">Tworzenie dysku zarządzanego z wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="29ce1-122">Create a managed disk from a VHD</span></span>](virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[<span data-ttu-id="29ce1-123">Utwórz maszynę wirtualną z dyskiem zarządzanym</span><span class="sxs-lookup"><span data-stu-id="29ce1-123">Create a virtual machine from a managed disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="29ce1-124">Aby uzyskać więcej informacji dotyczących modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="29ce1-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="29ce1-125">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w [dokumentacji maszyny Wirtualnej systemu Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="29ce1-125">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>