---
title: "Azure CLI przykładowym skrypcie - migawki eksportu/kopiowania jako dysk VHD do konta magazynu w innym regionie | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie - migawki eksportu/kopiowania jako dysk VHD do konta magazynu w tym samym lub różnych subskrypcji"
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
ms.openlocfilehash: a6ea65aba91641ece415db4df6ae9c17b42a0954
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-to-a-storage-account-in-different-region-with-cli"></a><span data-ttu-id="9d07d-103">Eksport/kopiowania zarządzane migawki jako dysk VHD do konta magazynu w innym regionie z interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="9d07d-103">Export/Copy managed snapshots as VHD to a storage account in different region with CLI</span></span>

<span data-ttu-id="9d07d-104">Ten skrypt eksportuje zarządzanych migawki na konto magazynu w innym regionie.</span><span class="sxs-lookup"><span data-stu-id="9d07d-104">This script exports a managed snapshot to a storage account in different region.</span></span> <span data-ttu-id="9d07d-105">Najpierw generuje identyfikator URI sygnatury dostępu Współdzielonego migawki, a następnie używa, aby skopiować go do konta magazynu w innym regionie.</span><span class="sxs-lookup"><span data-stu-id="9d07d-105">It first generates the SAS URI of the snapshot and then uses it to copy it to a storage account in different region.</span></span> <span data-ttu-id="9d07d-106">Użyj tego skryptu do obsługi kopii zapasowych dysków zarządzanych w innym regionie odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="9d07d-106">Use this script to maintain backup of your managed disks in different region for disaster recovery.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9d07d-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="9d07d-107">Sample script</span></span>

<span data-ttu-id="9d07d-108">[!code-azurecli[główne](../../../cli_scripts/virtual-machine/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "migawki kopiowania")]</span><span class="sxs-lookup"><span data-stu-id="9d07d-108">[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="9d07d-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="9d07d-109">Script explanation</span></span>

<span data-ttu-id="9d07d-110">Ten skrypt używa następujących poleceń, można wygenerować identyfikatora URI sygnatury dostępu Współdzielonego dla zarządzanych migawki i kopiuje migawki na konto magazynu przy użyciu identyfikatora URI połączenia SAS.</span><span class="sxs-lookup"><span data-stu-id="9d07d-110">This script uses following commands to generate SAS URI for a managed snapshot and copies the snapshot to a storage account using SAS URI.</span></span> <span data-ttu-id="9d07d-111">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="9d07d-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9d07d-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="9d07d-112">Command</span></span> | <span data-ttu-id="9d07d-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="9d07d-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9d07d-114">AZ migawki Udziel dostępu</span><span class="sxs-lookup"><span data-stu-id="9d07d-114">az snapshot grant-access</span></span>](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | <span data-ttu-id="9d07d-115">Generuje SAS tylko do odczytu, służący do skopiuj podstawowy plik VHD na konto magazynu lub pobrać go do lokalnego</span><span class="sxs-lookup"><span data-stu-id="9d07d-115">Generates read-only SAS that is used to copy underlying VHD file to a storage account or download it to on-premises</span></span>  |
| [<span data-ttu-id="9d07d-116">Uruchom kopiowania obiektu blob magazynu az</span><span class="sxs-lookup"><span data-stu-id="9d07d-116">az storage blob copy start</span></span>](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | <span data-ttu-id="9d07d-117">Asynchronicznie kopiuje obiektu blob z jednego konta magazynu do innego</span><span class="sxs-lookup"><span data-stu-id="9d07d-117">Copies a blob asynchronously from one storage account to another</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9d07d-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9d07d-118">Next steps</span></span>

[<span data-ttu-id="9d07d-119">Tworzenie dysku zarządzanego z wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="9d07d-119">Create a managed disk from a VHD</span></span>](virtual-machines-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[<span data-ttu-id="9d07d-120">Utwórz maszynę wirtualną z dyskiem zarządzanym</span><span class="sxs-lookup"><span data-stu-id="9d07d-120">Create a virtual machine from a managed disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="9d07d-121">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9d07d-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9d07d-122">Dodatkowe maszyny wirtualnej i dysków zarządzanych przykłady skryptów interfejsu wiersza polecenia można znaleźć w [dokumentacji maszyny Wirtualnej systemu Linux Azure](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9d07d-122">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
