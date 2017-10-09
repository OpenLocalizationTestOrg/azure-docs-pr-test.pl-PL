---
title: "Przykładowy skrypt interfejsu wiersza polecenia aaaAzure - ruchu sieciowego maszyn wirtualnych filtru | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: c2f14e54bc96c99420b4300d1c24a457ac8c948c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="eef84-103">Filtrowanie ruchu przychodzącego i wychodzącego ruchu sieciowego maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="eef84-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="eef84-104">Ten przykładowy skrypt tworzy sieć wirtualną z podsieci frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="eef84-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="eef84-105">Ruchu przychodzącego ruchu sieciowego podsieci frontonu toohello jest ograniczona tooHTTP, HTTPS i SSH, podczas gdy wychodzący ruch toohello Internet z podsieci wewnętrznej hello jest niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="eef84-105">Inbound network traffic toohello front-end subnet is limited tooHTTP, HTTPS and SSH, while outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> <span data-ttu-id="eef84-106">Po uruchomieniu skryptu hello, będziesz mieć jedną maszynę wirtualną z dwiema kartami sieciowymi.</span><span class="sxs-lookup"><span data-stu-id="eef84-106">After running hello script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="eef84-107">Poszczególne karty Sieciowe są połączone tooa innej podsieci.</span><span class="sxs-lookup"><span data-stu-id="eef84-107">Each NIC is connected tooa different subnet.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="eef84-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="eef84-108">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a><span data-ttu-id="eef84-109">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="eef84-109">Clean up deployment</span></span> 

<span data-ttu-id="eef84-110">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="eef84-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="eef84-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="eef84-111">Script explanation</span></span>

<span data-ttu-id="eef84-112">Ten skrypt używa powitania po toocreate poleceń, grupy zasobów, sieci wirtualnej i grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="eef84-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="eef84-113">Każde polecenie w dokumentacji konkretnego toocommand łącza tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="eef84-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="eef84-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="eef84-114">Command</span></span> | <span data-ttu-id="eef84-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="eef84-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="eef84-116">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="eef84-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="eef84-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="eef84-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="eef84-118">Tworzenie sieci wirtualnej sieci az</span><span class="sxs-lookup"><span data-stu-id="eef84-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="eef84-119">Tworzy sieć wirtualna platformy Azure i podsieci frontonu.</span><span class="sxs-lookup"><span data-stu-id="eef84-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="eef84-120">Utwórz podsieć sieci az</span><span class="sxs-lookup"><span data-stu-id="eef84-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="eef84-121">Tworzy podsieć zaplecza.</span><span class="sxs-lookup"><span data-stu-id="eef84-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="eef84-122">Aktualizacja podsieci sieci wirtualnej sieci az</span><span class="sxs-lookup"><span data-stu-id="eef84-122">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update) | <span data-ttu-id="eef84-123">Kojarzy toosubnets grup NSG.</span><span class="sxs-lookup"><span data-stu-id="eef84-123">Associates NSGs toosubnets.</span></span> |
| [<span data-ttu-id="eef84-124">Tworzenie sieci az publicznego ip</span><span class="sxs-lookup"><span data-stu-id="eef84-124">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="eef84-125">Tworzy publicznego adresu IP adres tooaccess hello maszyny Wirtualnej na podstawie hello Internet.</span><span class="sxs-lookup"><span data-stu-id="eef84-125">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="eef84-126">Utwórz az kart interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="eef84-126">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="eef84-127">Tworzy interfejsy sieci wirtualnej i dołącza je podsieci sieci wirtualnej toohello frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="eef84-127">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="eef84-128">Tworzenie grupy nsg sieci az</span><span class="sxs-lookup"><span data-stu-id="eef84-128">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="eef84-129">Tworzy grupy zabezpieczeń sieci (NSG), które są skojarzone toohello podsieci frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="eef84-129">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="eef84-130">Tworzenie reguły nsg sieci az</span><span class="sxs-lookup"><span data-stu-id="eef84-130">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="eef84-131">Tworzy reguły NSG, które zezwala lub blokuje określone porty toospecific podsieci.</span><span class="sxs-lookup"><span data-stu-id="eef84-131">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="eef84-132">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="eef84-132">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="eef84-133">Tworzy maszyny wirtualne i dołącza tooeach karty Sieciowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eef84-133">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="eef84-134">To polecenie określa również toouse obrazu maszyny wirtualnej hello i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="eef84-134">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="eef84-135">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="eef84-135">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="eef84-136">Usuwa grupę zasobów i wszystkie zasoby, które zawiera.</span><span class="sxs-lookup"><span data-stu-id="eef84-136">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="eef84-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eef84-137">Next steps</span></span>

<span data-ttu-id="eef84-138">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="eef84-138">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="eef84-139">Dodatkowe przykłady skryptów sieci interfejsu wiersza polecenia można znaleźć w hello [Azure Przegląd dokumentacji](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="eef84-139">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
