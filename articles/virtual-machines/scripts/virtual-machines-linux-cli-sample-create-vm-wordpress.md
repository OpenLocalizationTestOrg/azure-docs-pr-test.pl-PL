---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Utwórz Maszynę wirtualną systemu Linux z WordPress | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Utwórz Maszynę wirtualną systemu Linux z WordPress"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 2c5c03d08b6d5d27eb8c505b1dbd817eda5f2fc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-wordpress"></a><span data-ttu-id="7152e-103">Utwórz maszynę Wirtualną z WordPress</span><span class="sxs-lookup"><span data-stu-id="7152e-103">Create a VM with WordPress</span></span>

<span data-ttu-id="7152e-104">Ten skrypt tworzy maszynę wirtualną, a następnie używa hello maszyny wirtualnej Azure skryptu niestandardowego rozszerzenia tooinstall WordPress.</span><span class="sxs-lookup"><span data-stu-id="7152e-104">This script creates a virtual machine, and then uses hello Azure Virtual Machine custom script extension tooinstall WordPress.</span></span> <span data-ttu-id="7152e-105">Po uruchamianie skryptu hello, można uzyskać dostępu do hello WordPress konfiguracji witryny na `http://<public IP of VM>/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="7152e-105">After running hello script, you can access hello WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="7152e-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="7152e-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7152e-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="7152e-107">Clean up deployment</span></span> 

<span data-ttu-id="7152e-108">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="7152e-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="7152e-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="7152e-109">Script explanation</span></span>

<span data-ttu-id="7152e-110">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów maszyny wirtualnej, a wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="7152e-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="7152e-111">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="7152e-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7152e-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="7152e-112">Command</span></span> | <span data-ttu-id="7152e-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="7152e-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7152e-114">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="7152e-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="7152e-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="7152e-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7152e-116">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="7152e-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="7152e-117">Tworzy maszynę wirtualną hello i łączy go toohello karty sieciowej, sieć wirtualną, podsieci i NSG.</span><span class="sxs-lookup"><span data-stu-id="7152e-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="7152e-118">To polecenie określa również toobe obrazu maszyny wirtualnej hello używane i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="7152e-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="7152e-119">open — port az maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7152e-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="7152e-120">Tworzy sieci zabezpieczeń grupy reguł tooallow ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="7152e-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="7152e-121">W tym przykładzie port 80 jest otwarty dla ruchu HTTP.</span><span class="sxs-lookup"><span data-stu-id="7152e-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="7152e-122">zestaw rozszerzeń maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="7152e-122">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="7152e-123">Dodaj maszynę wirtualną toohello niestandardowe rozszerzenie skryptu hello, która wywołuje skrypt tooinstall WordPress.</span><span class="sxs-lookup"><span data-stu-id="7152e-123">Add hello Custom Script Extension toohello virtual machine, which invokes a script tooinstall WordPress.</span></span> |
| [<span data-ttu-id="7152e-124">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="7152e-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="7152e-125">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="7152e-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7152e-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7152e-126">Next steps</span></span>

<span data-ttu-id="7152e-127">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7152e-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7152e-128">Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7152e-128">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
