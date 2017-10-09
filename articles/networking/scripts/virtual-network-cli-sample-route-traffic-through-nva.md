---
title: "Przykładowy skrypt interfejsu wiersza polecenia aaaAzure — ruch sieciowy przez urządzenie wirtualne sieci | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt usługi Azure interfejsu wiersza polecenia — ruch trasy przez urządzenie wirtualne zapory w sieci."
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
ms.openlocfilehash: 981d6073be04a7ebaf96b657fbab8a378e7a995e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="8c511-103">Kierować ruchem przez urządzenie wirtualne sieci</span><span class="sxs-lookup"><span data-stu-id="8c511-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="8c511-104">Ten przykładowy skrypt tworzy sieć wirtualną z podsieci frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="8c511-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="8c511-105">Tworzy również Maszynę wirtualną z tooroute włączone ruchu między dwiema podsieciami hello przekazywania pakietów IP.</span><span class="sxs-lookup"><span data-stu-id="8c511-105">It also creates a VM with IP forwarding enabled tooroute traffic between hello two subnets.</span></span> <span data-ttu-id="8c511-106">Po uruchomieniu skryptu hello można wdrażać oprogramowanie sieci, takie jak aplikacja zapory, toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8c511-106">After running hello script you can deploy network software, such as a firewall application, toohello VM.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="8c511-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="8c511-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a><span data-ttu-id="8c511-108">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="8c511-108">Clean up deployment</span></span> 

<span data-ttu-id="8c511-109">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="8c511-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="8c511-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="8c511-110">Script explanation</span></span>

<span data-ttu-id="8c511-111">Ten skrypt używa powitania po toocreate poleceń, grupy zasobów, sieci wirtualnej i grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="8c511-111">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="8c511-112">Każde polecenie w dokumentacji konkretnego toocommand łącza tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="8c511-112">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="8c511-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="8c511-113">Command</span></span> | <span data-ttu-id="8c511-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="8c511-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8c511-115">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="8c511-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="8c511-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="8c511-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8c511-117">Tworzenie sieci wirtualnej sieci az</span><span class="sxs-lookup"><span data-stu-id="8c511-117">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="8c511-118">Tworzy sieć wirtualna platformy Azure i podsieci frontonu.</span><span class="sxs-lookup"><span data-stu-id="8c511-118">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="8c511-119">Utwórz podsieć sieci az</span><span class="sxs-lookup"><span data-stu-id="8c511-119">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="8c511-120">Tworzy zaplecza i strefą DMZ podsieci.</span><span class="sxs-lookup"><span data-stu-id="8c511-120">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="8c511-121">Tworzenie sieci az publicznego ip</span><span class="sxs-lookup"><span data-stu-id="8c511-121">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="8c511-122">Tworzy publicznego adresu IP adres tooaccess hello maszyny Wirtualnej na podstawie hello Internet.</span><span class="sxs-lookup"><span data-stu-id="8c511-122">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="8c511-123">Utwórz az kart interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="8c511-123">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="8c511-124">Tworzy interfejs sieci wirtualnej i Włącz przesyłanie dalej IP dla niego.</span><span class="sxs-lookup"><span data-stu-id="8c511-124">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="8c511-125">Tworzenie grupy nsg sieci az</span><span class="sxs-lookup"><span data-stu-id="8c511-125">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="8c511-126">Tworzy sieciową grupę zabezpieczeń (NSG).</span><span class="sxs-lookup"><span data-stu-id="8c511-126">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="8c511-127">Tworzenie reguły nsg sieci az</span><span class="sxs-lookup"><span data-stu-id="8c511-127">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) | <span data-ttu-id="8c511-128">Tworzy reguły NSG, które zezwala na portach HTTP i HTTPS ruchu przychodzącego toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8c511-128">Creates NSG rules that allow HTTP and HTTPS ports inbound toohello VM.</span></span> |
| [<span data-ttu-id="8c511-129">Aktualizacja podsieci sieci wirtualnej sieci az</span><span class="sxs-lookup"><span data-stu-id="8c511-129">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update)| <span data-ttu-id="8c511-130">Grupy NSG hello stowarzyszonych i toosubnets tabele tras.</span><span class="sxs-lookup"><span data-stu-id="8c511-130">Associates hello NSGs and route tables toosubnets.</span></span> |
| [<span data-ttu-id="8c511-131">Utwórz tabelę tras az sieci</span><span class="sxs-lookup"><span data-stu-id="8c511-131">az network route-table create</span></span>](/cli/azure/network/route-table#create)| <span data-ttu-id="8c511-132">Tworzy tabelę tras dla wszystkich tras.</span><span class="sxs-lookup"><span data-stu-id="8c511-132">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="8c511-133">Utwórz trasę tabeli tras sieciowych az</span><span class="sxs-lookup"><span data-stu-id="8c511-133">az network route-table route create</span></span>](/cli/azure/network/route-table/route#create)| <span data-ttu-id="8c511-134">Tworzy tras tooroute ruch między podsieciami i hello Internet za pośrednictwem hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8c511-134">Creates routes tooroute traffic between subnets and hello Internet through hello VM.</span></span> |
| [<span data-ttu-id="8c511-135">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="8c511-135">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="8c511-136">Tworzy maszynę wirtualną i dołącza hello tooit karty Sieciowej.</span><span class="sxs-lookup"><span data-stu-id="8c511-136">Creates a virtual machine and attaches hello NIC tooit.</span></span> <span data-ttu-id="8c511-137">To polecenie określa również toouse obrazu maszyny wirtualnej hello i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="8c511-137">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="8c511-138">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="8c511-138">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="8c511-139">Usuwa grupę zasobów i wszystkie zasoby, które zawiera.</span><span class="sxs-lookup"><span data-stu-id="8c511-139">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8c511-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8c511-140">Next steps</span></span>

<span data-ttu-id="8c511-141">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8c511-141">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="8c511-142">Dodatkowe przykłady skryptów sieci interfejsu wiersza polecenia można znaleźć w hello [Azure Przegląd dokumentacji](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="8c511-142">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
