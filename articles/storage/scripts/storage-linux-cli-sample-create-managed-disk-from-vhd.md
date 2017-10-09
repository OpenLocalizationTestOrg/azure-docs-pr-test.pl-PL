---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Tworzenie dysku zarządzanego z pliku VHD na koncie magazynu w hello tej samej subskrypcji | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — tworzenie dysków zarządzanych z pliku VHD na koncie magazynu w hello tej samej subskrypcji"
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
ms.openlocfilehash: 1e792fdbb7daea92bf6a6589a5d8aab5b9b5a670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-hello-same-subscription-with-cli"></a><span data-ttu-id="fe4e7-103">Tworzenie dysku zarządzanego z pliku VHD na koncie magazynu w hello tej samej subskrypcji z interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="fe4e7-103">Create a managed disk from a VHD file in a storage account in hello same subscription with CLI</span></span>

<span data-ttu-id="fe4e7-104">Ten skrypt tworzy dysków zarządzanych z pliku VHD na koncie magazynu w hello tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="fe4e7-104">This script creates a managed disk from a VHD file in a storage account in hello same subscription.</span></span> <span data-ttu-id="fe4e7-105">Użyj tego skryptu tooimport specjalne (nie uogólniony/Sysprep) wirtualnego dysku twardego toomanaged OS dysku toocreate maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fe4e7-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD toomanaged OS disk toocreate a virtual machine.</span></span> <span data-ttu-id="fe4e7-106">Możesz też użyć go tooimport dysku danych toomanaged dane wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="fe4e7-106">Or, use it tooimport a data VHD toomanaged data disk.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fe4e7-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="fe4e7-107">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="fe4e7-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="fe4e7-108">Script explanation</span></span>

<span data-ttu-id="fe4e7-109">Ten skrypt używa następujących poleceń toocreate dysków zarządzanych z dysku VHD.</span><span class="sxs-lookup"><span data-stu-id="fe4e7-109">This script uses following commands toocreate a managed disk from a VHD.</span></span> <span data-ttu-id="fe4e7-110">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="fe4e7-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fe4e7-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="fe4e7-111">Command</span></span> | <span data-ttu-id="fe4e7-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="fe4e7-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fe4e7-113">Tworzenie dysku az</span><span class="sxs-lookup"><span data-stu-id="fe4e7-113">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="fe4e7-114">Tworzy dysków zarządzanych przy użyciu identyfikatora URI dysku VHD na koncie magazynu w hello tej samej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="fe4e7-114">Creates a managed disk using URI of a VHD in a storage account in hello same subscription</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fe4e7-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fe4e7-115">Next steps</span></span>

[<span data-ttu-id="fe4e7-116">Utwórz maszynę wirtualną, dołączając dysków zarządzanych jako dysk systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="fe4e7-116">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="fe4e7-117">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fe4e7-117">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fe4e7-118">Dodatkowe maszyny wirtualnej i dysków zarządzanych przykłady skryptów interfejsu wiersza polecenia można znaleźć w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe4e7-118">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
