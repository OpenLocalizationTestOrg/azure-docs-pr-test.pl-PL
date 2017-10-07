---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Utwórz dwie maszyny wirtualne z wewnętrznych i zewnętrznych grupy NSG | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Utwórz dwie maszyny wirtualne z wewnętrznych i zewnętrznych NSG"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: f04e62d09575bee34ac4aeee949736b34000c337
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a><span data-ttu-id="0e616-103">Bezpieczny ruch sieciowy między maszynami wirtualnymi</span><span class="sxs-lookup"><span data-stu-id="0e616-103">Secure network traffic between virtual machines</span></span>

<span data-ttu-id="0e616-104">Ten skrypt tworzy dwie maszyny wirtualne i zabezpiecza tooboth ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="0e616-104">This script creates two virtual machines and secures incoming traffic tooboth.</span></span> <span data-ttu-id="0e616-105">Witaj jednej maszyny wirtualnej jest dostępny z Internetu i grupy zabezpieczeń sieci (NSG) skonfigurował tooallow ruchu na portu 3389 i portu 80.</span><span class="sxs-lookup"><span data-stu-id="0e616-105">One virtual machine is accessible on hello internet and has a network security group (NSG) configured tooallow traffic on port 3389 and port 80.</span></span> <span data-ttu-id="0e616-106">Witaj drugiej maszyny wirtualnej nie jest dostępny na hello internet i tooonly NSG skonfigurowane ma zezwalać na ruch z hello na pierwszej maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0e616-106">hello second virtual machine is not accessible on hello internet, and has an NSG configured tooonly allow traffic from hello first virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="0e616-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="0e616-107">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-windows-vm-nsg.sh "Create VM with NSG")]

## <a name="clean-up-deployment"></a><span data-ttu-id="0e616-108">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="0e616-108">Clean up deployment</span></span> 

<span data-ttu-id="0e616-109">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="0e616-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="0e616-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="0e616-110">Script explanation</span></span>

<span data-ttu-id="0e616-111">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów maszyny wirtualnej, a wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="0e616-111">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="0e616-112">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="0e616-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0e616-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="0e616-113">Command</span></span> | <span data-ttu-id="0e616-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="0e616-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0e616-115">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="0e616-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="0e616-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="0e616-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0e616-117">Tworzenie sieci wirtualnej sieci az</span><span class="sxs-lookup"><span data-stu-id="0e616-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="0e616-118">Tworzy sieć wirtualna platformy Azure i podsieć.</span><span class="sxs-lookup"><span data-stu-id="0e616-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="0e616-119">Utwórz az podsieci sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="0e616-119">az network vnet subnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="0e616-120">Tworzy podsieć.</span><span class="sxs-lookup"><span data-stu-id="0e616-120">Creates a subnet.</span></span> |
| [<span data-ttu-id="0e616-121">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="0e616-121">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="0e616-122">Tworzy maszynę wirtualną hello i łączy go toohello karty sieciowej, sieć wirtualną, podsieci i NSG.</span><span class="sxs-lookup"><span data-stu-id="0e616-122">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="0e616-123">To polecenie określa również toobe obrazu maszyny wirtualnej hello używane i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="0e616-123">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="0e616-124">Aktualizacja reguły nsg sieci az</span><span class="sxs-lookup"><span data-stu-id="0e616-124">az network nsg rule update</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | <span data-ttu-id="0e616-125">Aktualizuje reguły NSG.</span><span class="sxs-lookup"><span data-stu-id="0e616-125">Updates an NSG rule.</span></span> <span data-ttu-id="0e616-126">W tym przykładzie reguła zaplecza hello jest zaktualizowane toopass ruch tylko z podsieci frontonu hello.</span><span class="sxs-lookup"><span data-stu-id="0e616-126">In this sample, hello back-end rule is updated toopass through traffic only from hello front-end subnet.</span></span> |
| [<span data-ttu-id="0e616-127">Lista reguł nsg sieci az</span><span class="sxs-lookup"><span data-stu-id="0e616-127">az network nsg rule list</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | <span data-ttu-id="0e616-128">Zwraca informacje dotyczące reguły grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="0e616-128">Returns information about a network security group rule.</span></span> <span data-ttu-id="0e616-129">W tym przykładzie nazwa reguły hello jest przechowywana w zmiennej do użycia później w skrypcie hello.</span><span class="sxs-lookup"><span data-stu-id="0e616-129">In this sample, hello rule name is stored in a variable for use later in hello script.</span></span> |
| [<span data-ttu-id="0e616-130">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="0e616-130">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="0e616-131">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="0e616-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0e616-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0e616-132">Next steps</span></span>

<span data-ttu-id="0e616-133">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0e616-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0e616-134">Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0e616-134">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
