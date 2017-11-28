---
title: "Azure CLI przykładowym skrypcie - migawki kopiowania (przenoszenia) dysków zarządzanych do tych samych lub różnych subskrypcji z interfejsu wiersza polecenia | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie - migawki kopiowania (przenoszenia) dysków zarządzanych do tych samych lub różnych subskrypcji z interfejsu wiersza polecenia"
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
ms.openlocfilehash: 0127e342bd0c3afbe9de775399f5510814bff499
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="copy-snapshot-of-a-managed-disk-to-same-or-different-subscription-with-cli"></a><span data-ttu-id="57865-103">Kopiowanie migawek dysków zarządzanych do tych samych lub różnych subskrypcji z interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="57865-103">Copy snapshot of a managed disk to same or different subscription with CLI</span></span>

<span data-ttu-id="57865-104">Ten skrypt powoduje skopiowanie migawki dysków zarządzanych tych samych lub różnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="57865-104">This script copies a snapshot of a managed disk to same or different subscription.</span></span> <span data-ttu-id="57865-105">Użyj tego skryptu można przenieść do innej subskrypcji w tym samym regionie co migawki nadrzędnego migawki.</span><span class="sxs-lookup"><span data-stu-id="57865-105">Use this script to move a snapshot to different subscription in the same region as the parent snapshot.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="57865-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="57865-106">Sample script</span></span>

<span data-ttu-id="57865-107">[!code-azurecli[główne](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "migawki kopiowania")]</span><span class="sxs-lookup"><span data-stu-id="57865-107">[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="57865-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="57865-108">Script explanation</span></span>

<span data-ttu-id="57865-109">Ten skrypt używa następujących poleceń do tworzenia migawek w subskrypcji docelowej przy użyciu identyfikatora migawki źródła.</span><span class="sxs-lookup"><span data-stu-id="57865-109">This script uses following commands to create a snapshot in the target subscription using the Id of the source snapshot.</span></span> <span data-ttu-id="57865-110">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="57865-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="57865-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="57865-111">Command</span></span> | <span data-ttu-id="57865-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="57865-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="57865-113">Pokaż migawki az</span><span class="sxs-lookup"><span data-stu-id="57865-113">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="57865-114">Pobiera właściwości migawki przy użyciu nazwy i właściwości grupy zasobów migawki.</span><span class="sxs-lookup"><span data-stu-id="57865-114">Gets all the properties of a snapshot using the name and resource group properties of the snapshot.</span></span> <span data-ttu-id="57865-115">Identyfikator jest używana do skopiowania migawki do innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="57865-115">Id property is used to copy the snapshot to different subscription.</span></span>  |
| [<span data-ttu-id="57865-116">Tworzenie migawki az</span><span class="sxs-lookup"><span data-stu-id="57865-116">az snapshot create</span></span>](https://docs.microsoft.com/cli/azure/snapshot#create) | <span data-ttu-id="57865-117">Kopiuje migawki przez tworzenie migawek w innej subskrypcji przy użyciu identyfikatora i nazwy migawki nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="57865-117">Copies a snapshot by creating a snapshot in different subscription using the Id and name of the parent snapshot.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="57865-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="57865-118">Next steps</span></span>

[<span data-ttu-id="57865-119">Utwórz maszynę wirtualną z migawki</span><span class="sxs-lookup"><span data-stu-id="57865-119">Create a virtual machine from a snapshot</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="57865-120">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="57865-120">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="57865-121">Dodatkowe maszyny wirtualnej i dysków zarządzanych przykłady skryptów interfejsu wiersza polecenia można znaleźć w [dokumentacji maszyny Wirtualnej systemu Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="57865-121">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
