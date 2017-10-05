---
title: "Azure CLI skrypt przykładowy — Utwórz maszynę Wirtualną, dołączając dysków zarządzanych jako dysk systemu operacyjnego | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Utwórz maszynę Wirtualną, dołączając dysków zarządzanych jako dysk systemu operacyjnego"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 18eefee869b243b35d4426c226eff5f48cd490a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a><span data-ttu-id="ba926-103">Utwórz maszynę wirtualną przy użyciu istniejącego dysku systemu operacyjnego zarządzanego z interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="ba926-103">Create a virtual machine using an existing managed OS disk with CLI</span></span>

<span data-ttu-id="ba926-104">Ten skrypt tworzy maszynę wirtualną, dołączając istniejący dysk zarządzane jako dysk systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="ba926-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="ba926-105">Użyj tego skryptu w poprzednich scenariuszach:</span><span class="sxs-lookup"><span data-stu-id="ba926-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="ba926-106">Tworzenie maszyny Wirtualnej z istniejącego zarządzanych dysk systemu operacyjnego, który został skopiowany z dysków zarządzanych w innej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ba926-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="ba926-107">Tworzenie maszyny Wirtualnej z istniejącego dysku zarządzanego utworzony na podstawie specjalne pliku wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="ba926-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="ba926-108">Tworzenie maszyny Wirtualnej z istniejącego zarządzanych dysk systemu operacyjnego, który został utworzony na podstawie migawki</span><span class="sxs-lookup"><span data-stu-id="ba926-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ba926-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="ba926-109">Sample script</span></span>

<span data-ttu-id="ba926-110">[!code-azurecli-interactive[główne](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Utwórz maszynę Wirtualną z dyskiem zarządzanym")]</span><span class="sxs-lookup"><span data-stu-id="ba926-110">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="ba926-111">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="ba926-111">Clean up deployment</span></span> 

<span data-ttu-id="ba926-112">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="ba926-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ba926-113">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="ba926-113">Script explanation</span></span>

<span data-ttu-id="ba926-114">Ten skrypt używa następujących poleceń get właściwości dysków zarządzanych, Dołącz dysków zarządzanych do nowej maszyny Wirtualnej i tworzenie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ba926-114">This script uses the following commands to get managed disk properties, attach a managed disk to a new VM and create a VM.</span></span> <span data-ttu-id="ba926-115">Każdy element w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="ba926-115">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ba926-116">Polecenie</span><span class="sxs-lookup"><span data-stu-id="ba926-116">Command</span></span> | <span data-ttu-id="ba926-117">Uwagi</span><span class="sxs-lookup"><span data-stu-id="ba926-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ba926-118">Pokaż dysku az</span><span class="sxs-lookup"><span data-stu-id="ba926-118">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="ba926-119">Pobiera właściwości dysków zarządzanych przy użyciu nazwy dysku i nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="ba926-119">Gets managed disk properties using disk name and resource group name.</span></span> <span data-ttu-id="ba926-120">Identyfikator jest używana do podłączenia dysków zarządzanych do nowej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ba926-120">Id property is used to attach a managed disk to a new VM</span></span> |
| [<span data-ttu-id="ba926-121">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="ba926-121">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="ba926-122">Tworzy Maszynę wirtualną przy użyciu zarządzanego dysku systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="ba926-122">Creates a VM using a managed OS disk</span></span> |
## <a name="next-steps"></a><span data-ttu-id="ba926-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ba926-123">Next steps</span></span>

<span data-ttu-id="ba926-124">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ba926-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ba926-125">Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ba926-125">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
