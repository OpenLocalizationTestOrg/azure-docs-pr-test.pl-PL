---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Utwórz maszynę Wirtualną, dołączając dysków zarządzanych jako dysk systemu operacyjnego | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 71fc5c6a577c64b913cfa35e99b2b9b75dea0c31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a><span data-ttu-id="25dfe-103">Utwórz maszynę wirtualną przy użyciu istniejącego dysku systemu operacyjnego zarządzanego z interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="25dfe-103">Create a virtual machine using an existing managed OS disk with CLI</span></span>

<span data-ttu-id="25dfe-104">Ten skrypt tworzy maszynę wirtualną, dołączając istniejący dysk zarządzane jako dysk systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="25dfe-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="25dfe-105">Użyj tego skryptu w poprzednich scenariuszach:</span><span class="sxs-lookup"><span data-stu-id="25dfe-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="25dfe-106">Tworzenie maszyny Wirtualnej z istniejącego zarządzanych dysk systemu operacyjnego, który został skopiowany z dysków zarządzanych w innej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="25dfe-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="25dfe-107">Tworzenie maszyny Wirtualnej z istniejącego dysku zarządzanego utworzony na podstawie specjalne pliku wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="25dfe-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="25dfe-108">Tworzenie maszyny Wirtualnej z istniejącego zarządzanych dysk systemu operacyjnego, który został utworzony na podstawie migawki</span><span class="sxs-lookup"><span data-stu-id="25dfe-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="25dfe-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="25dfe-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]

## <a name="clean-up-deployment"></a><span data-ttu-id="25dfe-110">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="25dfe-110">Clean up deployment</span></span> 

<span data-ttu-id="25dfe-111">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="25dfe-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="25dfe-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="25dfe-112">Script explanation</span></span>

<span data-ttu-id="25dfe-113">Ten skrypt używa hello następujące właściwości dysku tooget zarządzane poleceń, Dołącz tooa dysków zarządzanych w nowej maszyny Wirtualnej i tworzenie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="25dfe-113">This script uses hello following commands tooget managed disk properties, attach a managed disk tooa new VM and create a VM.</span></span> <span data-ttu-id="25dfe-114">Każdy element w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="25dfe-114">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="25dfe-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="25dfe-115">Command</span></span> | <span data-ttu-id="25dfe-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="25dfe-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="25dfe-117">Pokaż dysku az</span><span class="sxs-lookup"><span data-stu-id="25dfe-117">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="25dfe-118">Pobiera właściwości dysków zarządzanych przy użyciu nazwy dysku i nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="25dfe-118">Gets managed disk properties using disk name and resource group name.</span></span> <span data-ttu-id="25dfe-119">Identyfikator właściwości jest używane tooattach tooa dysków zarządzanych w nowej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="25dfe-119">Id property is used tooattach a managed disk tooa new VM</span></span> |
| [<span data-ttu-id="25dfe-120">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="25dfe-120">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="25dfe-121">Tworzy Maszynę wirtualną przy użyciu zarządzanego dysku systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="25dfe-121">Creates a VM using a managed OS disk</span></span> |
## <a name="next-steps"></a><span data-ttu-id="25dfe-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="25dfe-122">Next steps</span></span>

<span data-ttu-id="25dfe-123">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="25dfe-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="25dfe-124">Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="25dfe-124">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
