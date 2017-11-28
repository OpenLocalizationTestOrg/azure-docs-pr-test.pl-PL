---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia - migawki eksportu/kopiowania co konto magazynu tooa wirtualnego dysku twardego w innym regionie | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie - migawki eksportu/kopiowania co konto magazynu tooa wirtualnego dysku twardego w tych samych lub różnych subskrypcji"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: 027c5e588c4f10d64d125c17f4c78a7d8e1ef060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-cli"></a><span data-ttu-id="8bc8c-103">Eksport/kopiowania zarządzane migawki co konto magazynu tooa wirtualnego dysku twardego w innym regionie z interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="8bc8c-103">Export/Copy managed snapshots as VHD tooa storage account in different region with CLI</span></span>

<span data-ttu-id="8bc8c-104">Ten skrypt eksportuje migawki zarządzanego konta magazynu tooa w innym regionie.</span><span class="sxs-lookup"><span data-stu-id="8bc8c-104">This script exports a managed snapshot tooa storage account in different region.</span></span> <span data-ttu-id="8bc8c-105">Najpierw generuje hello identyfikatora URI połączenia SAS hello migawki, a następnie używa go po toocopy go tooa konta magazynu w innym regionie.</span><span class="sxs-lookup"><span data-stu-id="8bc8c-105">It first generates hello SAS URI of hello snapshot and then uses it toocopy it tooa storage account in different region.</span></span> <span data-ttu-id="8bc8c-106">Użyj tej kopii zapasowej toomaintain skryptu dysków zarządzanych w innym regionie odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="8bc8c-106">Use this script toomaintain backup of your managed disks in different region for disaster recovery.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="8bc8c-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="8bc8c-107">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="8bc8c-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="8bc8c-108">Script explanation</span></span>

<span data-ttu-id="8bc8c-109">Ten skrypt używa następujących poleceń toogenerate identyfikator URI sygnatury dostępu Współdzielonego dla zarządzanych hello migawki i kopii migawki tooa konto magazynu przy użyciu identyfikatora URI połączenia SAS.</span><span class="sxs-lookup"><span data-stu-id="8bc8c-109">This script uses following commands toogenerate SAS URI for a managed snapshot and copies hello snapshot tooa storage account using SAS URI.</span></span> <span data-ttu-id="8bc8c-110">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="8bc8c-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="8bc8c-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="8bc8c-111">Command</span></span> | <span data-ttu-id="8bc8c-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="8bc8c-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8bc8c-113">AZ migawki Udziel dostępu</span><span class="sxs-lookup"><span data-stu-id="8bc8c-113">az snapshot grant-access</span></span>](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | <span data-ttu-id="8bc8c-114">Generuje SAS tylko do odczytu, używane toocopy podstawowego konta magazynu tooa pliku wirtualnego dysku twardego lub pobrać ją tooon lokalnych</span><span class="sxs-lookup"><span data-stu-id="8bc8c-114">Generates read-only SAS that is used toocopy underlying VHD file tooa storage account or download it tooon-premises</span></span>  |
| [<span data-ttu-id="8bc8c-115">Uruchom kopiowania obiektu blob magazynu az</span><span class="sxs-lookup"><span data-stu-id="8bc8c-115">az storage blob copy start</span></span>](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | <span data-ttu-id="8bc8c-116">Kopiuje obiekt blob asynchronicznie z jednego tooanother konta magazynu</span><span class="sxs-lookup"><span data-stu-id="8bc8c-116">Copies a blob asynchronously from one storage account tooanother</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8bc8c-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8bc8c-117">Next steps</span></span>

[<span data-ttu-id="8bc8c-118">Tworzenie dysku zarządzanego z wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="8bc8c-118">Create a managed disk from a VHD</span></span>](./../scripts/storage-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[<span data-ttu-id="8bc8c-119">Utwórz maszynę wirtualną z dyskiem zarządzanym</span><span class="sxs-lookup"><span data-stu-id="8bc8c-119">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="8bc8c-120">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8bc8c-120">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8bc8c-121">Dodatkowe maszyny wirtualnej i dysków zarządzanych przykłady skryptów interfejsu wiersza polecenia można znaleźć w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8bc8c-121">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
