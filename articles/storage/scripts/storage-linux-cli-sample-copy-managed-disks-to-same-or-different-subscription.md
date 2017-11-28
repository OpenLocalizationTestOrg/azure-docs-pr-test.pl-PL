---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia - kopiowania (przenoszenia) zarządzane toosame dysków lub innej subskrypcji | Dokumentacja firmy Microsoft"
description: "Azure przykładowym skrypcie interfejsu wiersza polecenia - toosame dysków zarządzanych kopiowania (przenoszenia) lub innej subskrypcji"
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
ms.openlocfilehash: 8581169baa0fd0e0eec1c72eab77b657f48b1cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-toosame-or-different-subscription-with-cli"></a><span data-ttu-id="f7457-103">Kopiowanie dysków zarządzanych toosame lub innej subskrypcji z interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="f7457-103">Copy managed disks toosame or different subscription with CLI</span></span>

<span data-ttu-id="f7457-104">Ten skrypt kopiuje toosame dysków zarządzanych lub innej subskrypcji, ale w hello sam region.</span><span class="sxs-lookup"><span data-stu-id="f7457-104">This script copies a managed disk toosame or different subscription but in hello same region.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f7457-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="f7457-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]


## <a name="script-explanation"></a><span data-ttu-id="f7457-106">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="f7457-106">Script explanation</span></span>

<span data-ttu-id="f7457-107">Ten skrypt używa następujących poleceń toocreate nowy dysk zarządzanych za pomocą subskrypcji docelowej hello hello identyfikator źródła hello zarządzane dysku.</span><span class="sxs-lookup"><span data-stu-id="f7457-107">This script uses following commands toocreate a new managed disk in hello target subscription using hello Id of hello source managed disk.</span></span> <span data-ttu-id="f7457-108">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="f7457-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f7457-109">Polecenie</span><span class="sxs-lookup"><span data-stu-id="f7457-109">Command</span></span> | <span data-ttu-id="f7457-110">Uwagi</span><span class="sxs-lookup"><span data-stu-id="f7457-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f7457-111">Pokaż dysku az</span><span class="sxs-lookup"><span data-stu-id="f7457-111">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="f7457-112">Pobiera wszystkie właściwości hello dysków zarządzanych przy użyciu właściwości hello nazwy i zasobów grupy hello dysku zarządzanego.</span><span class="sxs-lookup"><span data-stu-id="f7457-112">Gets all hello properties of a managed disk using hello name and resource group properties of hello managed disk.</span></span> <span data-ttu-id="f7457-113">Identyfikator właściwości jest używane toocopy hello zarządzane dysku toodifferent subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f7457-113">Id property is used toocopy hello managed disk toodifferent subscription.</span></span>  |
| [<span data-ttu-id="f7457-114">Tworzenie dysku az</span><span class="sxs-lookup"><span data-stu-id="f7457-114">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="f7457-115">Kopiuje dysków zarządzanych przez utworzenie nowych dysków zarządzanych w innej subskrypcji przy użyciu identyfikatora i nazwy nadrzędnego hello zarządzane dysku.</span><span class="sxs-lookup"><span data-stu-id="f7457-115">Copies a managed disk by creating a new managed disk in different subscription using Id and name hello parent managed disk.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="f7457-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f7457-116">Next steps</span></span>

[<span data-ttu-id="f7457-117">Utwórz maszynę wirtualną z dyskiem zarządzanym</span><span class="sxs-lookup"><span data-stu-id="f7457-117">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="f7457-118">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f7457-118">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f7457-119">Dodatkowe maszyny wirtualnej i dysków zarządzanych przykłady skryptów interfejsu wiersza polecenia można znaleźć w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7457-119">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
