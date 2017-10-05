---
title: "Azure CLI przykładowym skrypcie - dyskach do tych samych lub różnych subskrypcji zarządzanych kopiowania (przenoszenia) | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie - kopiowania (przenoszenia) zarządzanych dysków do tych samych lub różnych subskrypcji."
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
ms.openlocfilehash: 784ad81db2c83da14665fa926425928f12a15c27
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="copy-managed-disks-to-same-or-different-subscription-with-cli"></a><span data-ttu-id="7655c-103">Kopiowanie dysków zarządzanych do tych samych lub różnych subskrypcji z interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="7655c-103">Copy managed disks to same or different subscription with CLI</span></span>

<span data-ttu-id="7655c-104">Ten skrypt powoduje skopiowanie dysków zarządzanych do tych samych lub różnych subskrypcji, ale w tym samym regionie.</span><span class="sxs-lookup"><span data-stu-id="7655c-104">This script copies a managed disk to same or different subscription but in the same region.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="7655c-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="7655c-105">Sample script</span></span>

<span data-ttu-id="7655c-106">[!code-azurecli[główne](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "kopiowania zarządzane dysku")]</span><span class="sxs-lookup"><span data-stu-id="7655c-106">[!code-azurecli[main](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="7655c-107">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="7655c-107">Script explanation</span></span>

<span data-ttu-id="7655c-108">Ten skrypt używa następujących poleceń do tworzenia nowych dysków zarządzanych w subskrypcji docelowej przy użyciu identyfikatora dysków zarządzanych w źródłowym.</span><span class="sxs-lookup"><span data-stu-id="7655c-108">This script uses following commands to create a new managed disk in the target subscription using the Id of the source managed disk.</span></span> <span data-ttu-id="7655c-109">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="7655c-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="7655c-110">Polecenie</span><span class="sxs-lookup"><span data-stu-id="7655c-110">Command</span></span> | <span data-ttu-id="7655c-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="7655c-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7655c-112">Pokaż dysku az</span><span class="sxs-lookup"><span data-stu-id="7655c-112">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="7655c-113">Pobiera właściwości dysków zarządzanych przy użyciu nazwy i właściwości grupy zasobów dysku zarządzanego.</span><span class="sxs-lookup"><span data-stu-id="7655c-113">Gets all the properties of a managed disk using the name and resource group properties of the managed disk.</span></span> <span data-ttu-id="7655c-114">Identyfikator jest używana do kopiowania dysków zarządzanych do innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7655c-114">Id property is used to copy the managed disk to different subscription.</span></span>  |
| [<span data-ttu-id="7655c-115">Tworzenie dysku az</span><span class="sxs-lookup"><span data-stu-id="7655c-115">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="7655c-116">Kopie dysków zarządzanych przez utworzenie nowego zarządzanego dysku w innej subskrypcji przy użyciu identyfikatora i nazwy dysków zarządzanych w nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="7655c-116">Copies a managed disk by creating a new managed disk in different subscription using Id and name the parent managed disk.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="7655c-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7655c-117">Next steps</span></span>

[<span data-ttu-id="7655c-118">Utwórz maszynę wirtualną z dyskiem zarządzanym</span><span class="sxs-lookup"><span data-stu-id="7655c-118">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="7655c-119">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7655c-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7655c-120">Dodatkowe maszyny wirtualnej i dysków zarządzanych przykłady skryptów interfejsu wiersza polecenia można znaleźć w [dokumentacji maszyny Wirtualnej systemu Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7655c-120">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
