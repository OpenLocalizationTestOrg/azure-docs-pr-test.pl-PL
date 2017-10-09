---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Szybkie tworzenie maszyny Wirtualnej systemu Windows Server 2016 | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt Azure CLI — szybkie tworzenie maszyny Wirtualnej systemu Windows Server 2016"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rickstercdn
ms.openlocfilehash: 4c736ce9e2ecc9ee75b34f903cad52c9c0ee0707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="quick-create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="d3d56-103">Szybkie tworzenie maszyny wirtualnej z hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d3d56-103">Quick Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="d3d56-104">Ten skrypt tworzy maszynę wirtualną platformy Azure z systemem Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="d3d56-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="d3d56-105">Po uruchomieniu skryptu hello, można uzyskać dostępu do maszyny wirtualnej hello za pomocą połączenia pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="d3d56-105">After running hello script, you can access hello virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d3d56-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="d3d56-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-windows-vm-quick.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d3d56-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="d3d56-107">Clean up deployment</span></span> 

<span data-ttu-id="d3d56-108">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="d3d56-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="d3d56-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="d3d56-109">Script explanation</span></span>

<span data-ttu-id="d3d56-110">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów maszyny wirtualnej, a wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="d3d56-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="d3d56-111">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="d3d56-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d3d56-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="d3d56-112">Command</span></span> | <span data-ttu-id="d3d56-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d3d56-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d3d56-114">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="d3d56-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d3d56-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="d3d56-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d3d56-116">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="d3d56-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="d3d56-117">Tworzy maszynę wirtualną hello i łączy go toohello karty sieciowej, sieć wirtualną, podsieci i grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="d3d56-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="d3d56-118">To polecenie określa również toobe obrazu maszyny wirtualnej hello używane i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="d3d56-118">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="d3d56-119">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="d3d56-119">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="d3d56-120">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="d3d56-120">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d3d56-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d3d56-121">Next steps</span></span>

<span data-ttu-id="d3d56-122">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d3d56-122">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d3d56-123">Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d3d56-123">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
