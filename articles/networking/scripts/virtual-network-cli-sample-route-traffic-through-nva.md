---
title: "Azure CLI przykładowym skrypcie — ruch sieciowy przez urządzenie wirtualne sieci | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 78091b515c00591a4af8d807945475b6be50188a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="d2647-103">Kierować ruchem przez urządzenie wirtualne sieci</span><span class="sxs-lookup"><span data-stu-id="d2647-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="d2647-104">Ten przykładowy skrypt tworzy sieć wirtualną z podsieci frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="d2647-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="d2647-105">Tworzy również Maszynę wirtualną z przekazywanie IP jest włączone, można kierować ruchem między dwiema podsieciami.</span><span class="sxs-lookup"><span data-stu-id="d2647-105">It also creates a VM with IP forwarding enabled to route traffic between the two subnets.</span></span> <span data-ttu-id="d2647-106">Po uruchomieniu skryptu można wdrażać oprogramowanie sieci, takie jak aplikacja zapory, do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d2647-106">After running the script you can deploy network software, such as a firewall application, to the VM.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="d2647-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="d2647-107">Sample script</span></span>


<span data-ttu-id="d2647-108">[!code-azurecli-interactive[główne](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "kierować ruchem przez urządzenie wirtualne sieci")]</span><span class="sxs-lookup"><span data-stu-id="d2647-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d2647-109">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="d2647-109">Clean up deployment</span></span> 

<span data-ttu-id="d2647-110">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="d2647-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="d2647-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="d2647-111">Script explanation</span></span>

<span data-ttu-id="d2647-112">Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, sieć wirtualną i grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="d2647-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="d2647-113">Każde polecenie w tabeli łącza do dokumentacji specyficzne dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="d2647-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="d2647-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="d2647-114">Command</span></span> | <span data-ttu-id="d2647-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d2647-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d2647-116">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="d2647-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="d2647-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="d2647-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d2647-118">Tworzenie sieci wirtualnej sieci az</span><span class="sxs-lookup"><span data-stu-id="d2647-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="d2647-119">Tworzy sieć wirtualna platformy Azure i podsieci frontonu.</span><span class="sxs-lookup"><span data-stu-id="d2647-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="d2647-120">Utwórz podsieć sieci az</span><span class="sxs-lookup"><span data-stu-id="d2647-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="d2647-121">Tworzy zaplecza i strefą DMZ podsieci.</span><span class="sxs-lookup"><span data-stu-id="d2647-121">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="d2647-122">Tworzenie sieci az publicznego ip</span><span class="sxs-lookup"><span data-stu-id="d2647-122">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="d2647-123">Tworzy publiczny adres IP na dostęp do maszyny Wirtualnej z Internetu.</span><span class="sxs-lookup"><span data-stu-id="d2647-123">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="d2647-124">Utwórz az kart interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="d2647-124">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="d2647-125">Tworzy interfejs sieci wirtualnej i Włącz przesyłanie dalej IP dla niego.</span><span class="sxs-lookup"><span data-stu-id="d2647-125">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="d2647-126">Tworzenie grupy nsg sieci az</span><span class="sxs-lookup"><span data-stu-id="d2647-126">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="d2647-127">Tworzy sieciową grupę zabezpieczeń (NSG).</span><span class="sxs-lookup"><span data-stu-id="d2647-127">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="d2647-128">Tworzenie reguły nsg sieci az</span><span class="sxs-lookup"><span data-stu-id="d2647-128">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) | <span data-ttu-id="d2647-129">Tworzy reguły NSG, które zezwala na portach HTTP i HTTPS ruchu przychodzącego do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d2647-129">Creates NSG rules that allow HTTP and HTTPS ports inbound to the VM.</span></span> |
| [<span data-ttu-id="d2647-130">Aktualizacja podsieci sieci wirtualnej sieci az</span><span class="sxs-lookup"><span data-stu-id="d2647-130">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update)| <span data-ttu-id="d2647-131">Powoduje skojarzenie grupy NSG i tabele tras do podsieci.</span><span class="sxs-lookup"><span data-stu-id="d2647-131">Associates the NSGs and route tables to subnets.</span></span> |
| [<span data-ttu-id="d2647-132">Utwórz tabelę tras az sieci</span><span class="sxs-lookup"><span data-stu-id="d2647-132">az network route-table create</span></span>](/cli/azure/network/route-table#create)| <span data-ttu-id="d2647-133">Tworzy tabelę tras dla wszystkich tras.</span><span class="sxs-lookup"><span data-stu-id="d2647-133">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="d2647-134">Utwórz trasę tabeli tras sieciowych az</span><span class="sxs-lookup"><span data-stu-id="d2647-134">az network route-table route create</span></span>](/cli/azure/network/route-table/route#create)| <span data-ttu-id="d2647-135">Tworzy tras można kierować ruchem między podsieciami i Internetem za pośrednictwem maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d2647-135">Creates routes to route traffic between subnets and the Internet through the VM.</span></span> |
| [<span data-ttu-id="d2647-136">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="d2647-136">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="d2647-137">Tworzy maszynę wirtualną i dołącza do karty Sieciowej.</span><span class="sxs-lookup"><span data-stu-id="d2647-137">Creates a virtual machine and attaches the NIC to it.</span></span> <span data-ttu-id="d2647-138">To polecenie określa również obraz maszyny wirtualnej do użycia i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="d2647-138">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="d2647-139">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="d2647-139">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="d2647-140">Usuwa grupę zasobów i wszystkie zasoby, które zawiera.</span><span class="sxs-lookup"><span data-stu-id="d2647-140">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d2647-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d2647-141">Next steps</span></span>

<span data-ttu-id="d2647-142">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d2647-142">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="d2647-143">Dodatkowe przykłady skryptów sieci interfejsu wiersza polecenia można znaleźć w [Azure Przegląd dokumentacji](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="d2647-143">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>