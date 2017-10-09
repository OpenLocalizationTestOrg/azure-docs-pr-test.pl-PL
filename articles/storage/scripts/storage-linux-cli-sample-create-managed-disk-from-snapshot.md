---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Tworzenie dysku zarządzanego z migawki | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — tworzenie dysków zarządzanych z migawki"
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
ms.openlocfilehash: f92059353bfb739cff05213a9d206bfde2829a98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a><span data-ttu-id="daf23-103">Tworzenie dysku zarządzanego z migawki z interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="daf23-103">Create a managed disk from a snapshot with CLI</span></span>

<span data-ttu-id="daf23-104">Ten skrypt tworzy dysków zarządzanych z migawki.</span><span class="sxs-lookup"><span data-stu-id="daf23-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="daf23-105">Użyj toorestore maszynę wirtualną z migawek systemu operacyjnego i dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="daf23-105">Use it toorestore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="daf23-106">Utwórz systemu operacyjnego i danych zarządzanych dysków z odpowiednich migawki, a następnie utwórz nową maszynę wirtualną dołączając dysków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="daf23-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="daf23-107">Można także przywrócić dysków z danymi z istniejącej maszyny Wirtualnej, dołączając dyski danych utworzone na podstawie migawki.</span><span class="sxs-lookup"><span data-stu-id="daf23-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="daf23-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="daf23-108">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="daf23-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="daf23-109">Script explanation</span></span>

<span data-ttu-id="daf23-110">Ten skrypt używa następujących poleceń toocreate dysków zarządzanych z migawki.</span><span class="sxs-lookup"><span data-stu-id="daf23-110">This script uses following commands toocreate a managed disk from a snapshot.</span></span> <span data-ttu-id="daf23-111">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="daf23-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="daf23-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="daf23-112">Command</span></span> | <span data-ttu-id="daf23-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="daf23-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="daf23-114">Pokaż migawki az</span><span class="sxs-lookup"><span data-stu-id="daf23-114">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="daf23-115">Pobiera wszystkie właściwości hello migawki za pomocą hello nazwy i właściwości grupy zasobów hello migawki.</span><span class="sxs-lookup"><span data-stu-id="daf23-115">Gets all hello properties of a snapshot using hello name and resource group properties of hello snapshot.</span></span> <span data-ttu-id="daf23-116">Identyfikator właściwości jest używane toocreate dysków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="daf23-116">Id property is used toocreate managed disk.</span></span>  |
| [<span data-ttu-id="daf23-117">Tworzenie dysku az</span><span class="sxs-lookup"><span data-stu-id="daf23-117">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="daf23-118">Tworzy zarządzanego przy użyciu dysku migawki identyfikator migawki zarządzanych</span><span class="sxs-lookup"><span data-stu-id="daf23-118">Creates a managed disk using snapshot Id of a managed snapshot</span></span> |

## <a name="next-steps"></a><span data-ttu-id="daf23-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="daf23-119">Next steps</span></span>

[<span data-ttu-id="daf23-120">Utwórz maszynę wirtualną, dołączając dysków zarządzanych jako dysk systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="daf23-120">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="daf23-121">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="daf23-121">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="daf23-122">Dodatkowe maszyny wirtualnej i dysków zarządzanych przykłady skryptów interfejsu wiersza polecenia można znaleźć w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="daf23-122">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
