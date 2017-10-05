---
title: "Azure CLI skrypt przykładowy — Utwórz Maszynę wirtualną systemu Linux z WordPress | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: cc95a190b58cb208ac0b642fc9dc2253e993ca23
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-wordpress"></a><span data-ttu-id="6ef4e-103">Utwórz maszynę Wirtualną z WordPress</span><span class="sxs-lookup"><span data-stu-id="6ef4e-103">Create a VM with WordPress</span></span>

<span data-ttu-id="6ef4e-104">Ten skrypt tworzy maszynę wirtualną, a następnie używa maszyny wirtualnej Azure rozszerzenie skryptu niestandardowego do zainstalowania WordPress.</span><span class="sxs-lookup"><span data-stu-id="6ef4e-104">This script creates a virtual machine, and then uses the Azure Virtual Machine custom script extension to install WordPress.</span></span> <span data-ttu-id="6ef4e-105">Po uruchomieniu skryptu, można uzyskać dostępu do witrynę WordPress konfiguracji pod `http://<public IP of VM>/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="6ef4e-105">After running the script, you can access the WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6ef4e-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="6ef4e-106">Sample script</span></span>

<span data-ttu-id="6ef4e-107">[!code-azurecli-interactive[główne](../../../cli_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.sh "szybkie tworzenie maszyn wirtualnych")]</span><span class="sxs-lookup"><span data-stu-id="6ef4e-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6ef4e-108">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="6ef4e-108">Clean up deployment</span></span> 

<span data-ttu-id="6ef4e-109">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="6ef4e-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6ef4e-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="6ef4e-110">Script explanation</span></span>

<span data-ttu-id="6ef4e-111">Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, maszyny wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="6ef4e-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="6ef4e-112">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="6ef4e-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6ef4e-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="6ef4e-113">Command</span></span> | <span data-ttu-id="6ef4e-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6ef4e-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6ef4e-115">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="6ef4e-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6ef4e-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="6ef4e-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6ef4e-117">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="6ef4e-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="6ef4e-118">Tworzy maszynę wirtualną i podłączony do karty sieciowej, sieci wirtualnej, podsieci i NSG.</span><span class="sxs-lookup"><span data-stu-id="6ef4e-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="6ef4e-119">To polecenie określa również obraz maszyny wirtualnej ma być używany, a poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="6ef4e-119">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="6ef4e-120">open — port az maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6ef4e-120">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="6ef4e-121">Tworzy reguły grupy zabezpieczeń sieci, aby zezwalać na ruch przychodzący.</span><span class="sxs-lookup"><span data-stu-id="6ef4e-121">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="6ef4e-122">W tym przykładzie port 80 jest otwarty dla ruchu HTTP.</span><span class="sxs-lookup"><span data-stu-id="6ef4e-122">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="6ef4e-123">zestaw rozszerzeń maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="6ef4e-123">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="6ef4e-124">Dodaj niestandardowe rozszerzenie skryptu do maszyny wirtualnej, która wywołuje skrypt instalacji WordPress.</span><span class="sxs-lookup"><span data-stu-id="6ef4e-124">Add the Custom Script Extension to the virtual machine, which invokes a script to install WordPress.</span></span> |
| [<span data-ttu-id="6ef4e-125">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="6ef4e-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="6ef4e-126">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="6ef4e-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6ef4e-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6ef4e-127">Next steps</span></span>

<span data-ttu-id="6ef4e-128">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6ef4e-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6ef4e-129">Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6ef4e-129">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
