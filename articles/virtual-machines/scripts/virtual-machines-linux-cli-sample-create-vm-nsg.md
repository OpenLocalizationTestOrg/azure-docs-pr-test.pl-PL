---
title: "Azure CLI skrypt przykładowy — Utwórz dwie maszyny wirtualne z wewnętrznych i zewnętrznych grupy NSG | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Utwórz dwie maszyny wirtualne z wewnętrznych i zewnętrznych NSG"
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
ms.openlocfilehash: 7bd8c315ab0b7b3bcbbd9ebc8f17728079611f9c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a><span data-ttu-id="89a16-103">Bezpieczny ruch sieciowy między maszynami wirtualnymi</span><span class="sxs-lookup"><span data-stu-id="89a16-103">Secure network traffic between virtual machines</span></span>

<span data-ttu-id="89a16-104">Ten skrypt tworzy dwie maszyny wirtualne i zabezpiecza ruch przychodzący do obu.</span><span class="sxs-lookup"><span data-stu-id="89a16-104">This script creates two virtual machines and secures incoming traffic to both.</span></span> <span data-ttu-id="89a16-105">Jednej maszyny wirtualnej jest dostępny w Internecie i skonfigurował grupy zabezpieczeń sieci (NSG) tak, aby zezwolić na ruch na port 22 i portu 80.</span><span class="sxs-lookup"><span data-stu-id="89a16-105">One virtual machine is accessible on the internet and has a network security group (NSG) configured to allow traffic on port 22 and port 80.</span></span> <span data-ttu-id="89a16-106">Drugiej maszyny wirtualnej nie jest dostępny w Internecie, i ma skonfigurowane grupy NSG tylko zezwalająca na ruch z pierwszej maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="89a16-106">The second virtual machine is not accessible on the internet, and has an NSG configured to only allow traffic from the first virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="89a16-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="89a16-107">Sample script</span></span>

<span data-ttu-id="89a16-108">[!code-azurecli-interactive[główne](../../../cli_scripts/virtual-machine/create-vm-nsg/create-vm-nsg.sh "Utwórz maszynę Wirtualną z grupy NSG")]</span><span class="sxs-lookup"><span data-stu-id="89a16-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-vm-nsg.sh "Create VM with NSG")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="89a16-109">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="89a16-109">Clean up deployment</span></span> 

<span data-ttu-id="89a16-110">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="89a16-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="89a16-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="89a16-111">Script explanation</span></span>

<span data-ttu-id="89a16-112">Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, maszyny wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="89a16-112">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="89a16-113">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="89a16-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="89a16-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="89a16-114">Command</span></span> | <span data-ttu-id="89a16-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="89a16-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="89a16-116">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="89a16-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="89a16-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="89a16-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="89a16-118">Tworzenie sieci wirtualnej sieci az</span><span class="sxs-lookup"><span data-stu-id="89a16-118">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="89a16-119">Tworzy sieć wirtualna platformy Azure i podsieć.</span><span class="sxs-lookup"><span data-stu-id="89a16-119">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="89a16-120">Utwórz az podsieci sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="89a16-120">az network vnet subnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="89a16-121">Tworzy podsieć.</span><span class="sxs-lookup"><span data-stu-id="89a16-121">Creates a subnet.</span></span> |
| [<span data-ttu-id="89a16-122">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="89a16-122">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="89a16-123">Tworzy maszynę wirtualną i podłączony do karty sieciowej, sieci wirtualnej, podsieci i NSG.</span><span class="sxs-lookup"><span data-stu-id="89a16-123">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="89a16-124">To polecenie określa również obraz maszyny wirtualnej ma być używany, a poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="89a16-124">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="89a16-125">Lista reguł nsg sieci az</span><span class="sxs-lookup"><span data-stu-id="89a16-125">az network nsg rule list</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | <span data-ttu-id="89a16-126">Zwraca informacje dotyczące reguły grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="89a16-126">Returns information about a network security group rule.</span></span> <span data-ttu-id="89a16-127">W tym przykładzie nazwa reguły jest przechowywana w zmiennej do użycia później w skrypcie.</span><span class="sxs-lookup"><span data-stu-id="89a16-127">In this sample, the rule name is stored in a variable for use later in the script.</span></span> |
| [<span data-ttu-id="89a16-128">Aktualizacja reguły nsg sieci az</span><span class="sxs-lookup"><span data-stu-id="89a16-128">az network nsg rule update</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | <span data-ttu-id="89a16-129">Aktualizuje reguły NSG.</span><span class="sxs-lookup"><span data-stu-id="89a16-129">Updates an NSG rule.</span></span> <span data-ttu-id="89a16-130">W tym przykładzie jest aktualizowana reguła zaplecza, aby przekazywać ruch tylko z podsieci frontonu.</span><span class="sxs-lookup"><span data-stu-id="89a16-130">In this sample, the back-end rule is updated to pass through traffic only from the front-end subnet.</span></span> |
| [<span data-ttu-id="89a16-131">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="89a16-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="89a16-132">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="89a16-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="89a16-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="89a16-133">Next steps</span></span>

<span data-ttu-id="89a16-134">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="89a16-134">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="89a16-135">Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="89a16-135">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
