---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia - migawki kopiowania (przenoszenia) toosame dysków zarządzanych lub innej subskrypcji z interfejsu wiersza polecenia | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie - migawki kopiowania (przenoszenia) toosame dysków zarządzanych lub innej subskrypcji z interfejsu wiersza polecenia"
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
ms.openlocfilehash: 4a21fd2435181a033b563100888aba0c5834496d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-toosame-or-different-subscription-with-cli"></a><span data-ttu-id="be3c7-103">Kopiowanie migawek dysków zarządzanych w toosame lub innej subskrypcji z interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="be3c7-103">Copy snapshot of a managed disk toosame or different subscription with CLI</span></span>

<span data-ttu-id="be3c7-104">Ten skrypt kopiuje migawki dysków zarządzanych w toosame lub innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="be3c7-104">This script copies a snapshot of a managed disk toosame or different subscription.</span></span> <span data-ttu-id="be3c7-105">Użyj tego skryptu toomove subskrypcji toodifferent migawki w hello tego samego regionu hello nadrzędnego migawki.</span><span class="sxs-lookup"><span data-stu-id="be3c7-105">Use this script toomove a snapshot toodifferent subscription in hello same region as hello parent snapshot.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="be3c7-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="be3c7-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="be3c7-107">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="be3c7-107">Script explanation</span></span>

<span data-ttu-id="be3c7-108">Ten skrypt używa następujących poleceń toocreate migawki za pomocą subskrypcji docelowej hello hello identyfikator hello źródła migawki.</span><span class="sxs-lookup"><span data-stu-id="be3c7-108">This script uses following commands toocreate a snapshot in hello target subscription using hello Id of hello source snapshot.</span></span> <span data-ttu-id="be3c7-109">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="be3c7-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="be3c7-110">Polecenie</span><span class="sxs-lookup"><span data-stu-id="be3c7-110">Command</span></span> | <span data-ttu-id="be3c7-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="be3c7-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="be3c7-112">Pokaż migawki az</span><span class="sxs-lookup"><span data-stu-id="be3c7-112">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="be3c7-113">Pobiera wszystkie właściwości hello migawki za pomocą hello nazwy i właściwości grupy zasobów hello migawki.</span><span class="sxs-lookup"><span data-stu-id="be3c7-113">Gets all hello properties of a snapshot using hello name and resource group properties of hello snapshot.</span></span> <span data-ttu-id="be3c7-114">Identyfikator właściwości jest używane toocopy hello migawki toodifferent subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="be3c7-114">Id property is used toocopy hello snapshot toodifferent subscription.</span></span>  |
| [<span data-ttu-id="be3c7-115">Tworzenie migawki az</span><span class="sxs-lookup"><span data-stu-id="be3c7-115">az snapshot create</span></span>](https://docs.microsoft.com/cli/azure/snapshot#create) | <span data-ttu-id="be3c7-116">Kopie migawki przez tworzenie migawek w innej subskrypcji przy użyciu hello identyfikator i nazwa hello nadrzędnego migawki.</span><span class="sxs-lookup"><span data-stu-id="be3c7-116">Copies a snapshot by creating a snapshot in different subscription using hello Id and name of hello parent snapshot.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="be3c7-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="be3c7-117">Next steps</span></span>

[<span data-ttu-id="be3c7-118">Utwórz maszynę wirtualną z migawki</span><span class="sxs-lookup"><span data-stu-id="be3c7-118">Create a virtual machine from a snapshot</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="be3c7-119">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="be3c7-119">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="be3c7-120">Dodatkowe maszyny wirtualnej i dysków zarządzanych przykłady skryptów interfejsu wiersza polecenia można znaleźć w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="be3c7-120">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
