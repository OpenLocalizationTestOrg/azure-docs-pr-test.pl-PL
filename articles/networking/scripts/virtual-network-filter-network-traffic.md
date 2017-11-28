---
title: "Azure CLI przykładowym skrypcie - ruchu sieciowego maszyn wirtualnych filtr | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — filtrowania ruchu przychodzącego i wychodzącego ruchu sieciowego maszyny Wirtualnej."
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: 68ee013cff4e0be15af30239e0314f779f50177a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="10609-103">Filtrowanie ruchu przychodzącego i wychodzącego ruchu sieciowego maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="10609-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="10609-104">Ten przykładowy skrypt tworzy sieć wirtualną z podsieci frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="10609-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="10609-105">Ruch sieciowy przychodzący do podsieci frontonu może zawierać maksymalnie HTTP, HTTPS i SSH, gdy ruch wychodzący do Internetu z podsieci wewnętrznej jest niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="10609-105">Inbound network traffic to the front-end subnet is limited to HTTP, HTTPS and SSH, while outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> <span data-ttu-id="10609-106">Po uruchomieniu skryptu, ma jedną maszynę wirtualną z dwiema kartami sieciowymi.</span><span class="sxs-lookup"><span data-stu-id="10609-106">After running the script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="10609-107">Każda karta sieciowa jest podłączona do innej podsieci.</span><span class="sxs-lookup"><span data-stu-id="10609-107">Each NIC is connected to a different subnet.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="10609-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="10609-108">Sample script</span></span>


<span data-ttu-id="10609-109">[!code-azurecli-interactive[główne](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "ruchu sieciowego maszyn wirtualnych filtru")]</span><span class="sxs-lookup"><span data-stu-id="10609-109">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="10609-110">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="10609-110">Clean up deployment</span></span> 

<span data-ttu-id="10609-111">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="10609-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="10609-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="10609-112">Script explanation</span></span>

<span data-ttu-id="10609-113">Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, sieć wirtualną i grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="10609-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="10609-114">Każde polecenie w tabeli łącza do dokumentacji specyficzne dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="10609-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="10609-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="10609-115">Command</span></span> | <span data-ttu-id="10609-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="10609-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="10609-117">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="10609-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="10609-118">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="10609-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="10609-119">Tworzenie sieci wirtualnej sieci az</span><span class="sxs-lookup"><span data-stu-id="10609-119">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="10609-120">Tworzy sieć wirtualna platformy Azure i podsieci frontonu.</span><span class="sxs-lookup"><span data-stu-id="10609-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="10609-121">Utwórz podsieć sieci az</span><span class="sxs-lookup"><span data-stu-id="10609-121">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="10609-122">Tworzy podsieć zaplecza.</span><span class="sxs-lookup"><span data-stu-id="10609-122">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="10609-123">Aktualizacja podsieci sieci wirtualnej sieci az</span><span class="sxs-lookup"><span data-stu-id="10609-123">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update) | <span data-ttu-id="10609-124">Kojarzy grup NSG do podsieci.</span><span class="sxs-lookup"><span data-stu-id="10609-124">Associates NSGs to subnets.</span></span> |
| [<span data-ttu-id="10609-125">Tworzenie sieci az publicznego ip</span><span class="sxs-lookup"><span data-stu-id="10609-125">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="10609-126">Tworzy publiczny adres IP na dostęp do maszyny Wirtualnej z Internetu.</span><span class="sxs-lookup"><span data-stu-id="10609-126">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="10609-127">Utwórz az kart interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="10609-127">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="10609-128">Tworzy interfejsy sieci wirtualnej i dołącza je do podsieci sieci wirtualnej frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="10609-128">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="10609-129">Tworzenie grupy nsg sieci az</span><span class="sxs-lookup"><span data-stu-id="10609-129">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="10609-130">Tworzy sieciowej grupy zabezpieczeń (NSG), które są skojarzone z podsieci frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="10609-130">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="10609-131">Tworzenie reguły nsg sieci az</span><span class="sxs-lookup"><span data-stu-id="10609-131">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="10609-132">Tworzy reguły NSG, które zezwala lub blokuje określone porty do określonych podsieci.</span><span class="sxs-lookup"><span data-stu-id="10609-132">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="10609-133">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="10609-133">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="10609-134">Tworzy maszyny wirtualne i dołącza karty Sieciowej na każdej maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="10609-134">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="10609-135">To polecenie określa również obraz maszyny wirtualnej do użycia i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="10609-135">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="10609-136">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="10609-136">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="10609-137">Usuwa grupę zasobów i wszystkie zasoby, które zawiera.</span><span class="sxs-lookup"><span data-stu-id="10609-137">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="10609-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="10609-138">Next steps</span></span>

<span data-ttu-id="10609-139">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="10609-139">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="10609-140">Dodatkowe przykłady skryptów sieci interfejsu wiersza polecenia można znaleźć w [Azure Przegląd dokumentacji](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="10609-140">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>