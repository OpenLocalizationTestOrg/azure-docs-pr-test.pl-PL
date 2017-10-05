---
title: "Azure CLI skrypt przykładowy — tworzenie sieci dla aplikacji wielowarstwowych | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — tworzenie sieci wirtualnej dla aplikacji wielowarstwowych."
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
ms.openlocfilehash: de65d820f2d9eea49b58185c81d815675fd76740
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="50f61-103">Tworzenie sieci dla aplikacji wielowarstwowych</span><span class="sxs-lookup"><span data-stu-id="50f61-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="50f61-104">Ten przykładowy skrypt tworzy sieć wirtualną z podsieci frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="50f61-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="50f61-105">Ruch do podsieci frontonu jest ograniczona do HTTP i SSH, gdy ruch do podsieci wewnętrznej jest ograniczony do MySQL, port 3306.</span><span class="sxs-lookup"><span data-stu-id="50f61-105">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> <span data-ttu-id="50f61-106">Po uruchomieniu skryptu, masz dwie maszyny wirtualne, w każdej podsieci, którą można wdrożyć serwera sieci web i MySQL oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="50f61-106">After running the script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="50f61-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="50f61-107">Sample script</span></span>


<span data-ttu-id="50f61-108">[!code-azurecli-interactive[główne](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "sieci wirtualnej dla aplikacji wielowarstwowych")]</span><span class="sxs-lookup"><span data-stu-id="50f61-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="50f61-109">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="50f61-109">Clean up deployment</span></span> 

<span data-ttu-id="50f61-110">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="50f61-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="50f61-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="50f61-111">Script explanation</span></span>

<span data-ttu-id="50f61-112">Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, sieć wirtualną i grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="50f61-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="50f61-113">Każde polecenie w tabeli łącza do dokumentacji specyficzne dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="50f61-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="50f61-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="50f61-114">Command</span></span> | <span data-ttu-id="50f61-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="50f61-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="50f61-116">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="50f61-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="50f61-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="50f61-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="50f61-118">Tworzenie sieci wirtualnej sieci az</span><span class="sxs-lookup"><span data-stu-id="50f61-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="50f61-119">Tworzy sieć wirtualna platformy Azure i podsieci frontonu.</span><span class="sxs-lookup"><span data-stu-id="50f61-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="50f61-120">Utwórz podsieć sieci az</span><span class="sxs-lookup"><span data-stu-id="50f61-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="50f61-121">Tworzy podsieć zaplecza.</span><span class="sxs-lookup"><span data-stu-id="50f61-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="50f61-122">Tworzenie sieci az publicznego ip</span><span class="sxs-lookup"><span data-stu-id="50f61-122">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="50f61-123">Tworzy publiczny adres IP na dostęp do maszyny Wirtualnej z Internetu.</span><span class="sxs-lookup"><span data-stu-id="50f61-123">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="50f61-124">Utwórz az kart interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="50f61-124">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="50f61-125">Tworzy interfejsy sieci wirtualnej i dołącza je do podsieci sieci wirtualnej frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="50f61-125">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="50f61-126">Tworzenie grupy nsg sieci az</span><span class="sxs-lookup"><span data-stu-id="50f61-126">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="50f61-127">Tworzy sieciowej grupy zabezpieczeń (NSG), które są skojarzone z podsieci frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="50f61-127">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="50f61-128">Tworzenie reguły nsg sieci az</span><span class="sxs-lookup"><span data-stu-id="50f61-128">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="50f61-129">Tworzy reguły NSG, które zezwala lub blokuje określone porty do określonych podsieci.</span><span class="sxs-lookup"><span data-stu-id="50f61-129">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="50f61-130">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="50f61-130">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="50f61-131">Tworzy maszyny wirtualne i dołącza karty Sieciowej na każdej maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="50f61-131">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="50f61-132">To polecenie określa również obraz maszyny wirtualnej do użycia i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="50f61-132">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="50f61-133">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="50f61-133">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="50f61-134">Usuwa grupę zasobów i wszystkie zasoby, które zawiera.</span><span class="sxs-lookup"><span data-stu-id="50f61-134">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="50f61-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="50f61-135">Next steps</span></span>

<span data-ttu-id="50f61-136">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="50f61-136">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="50f61-137">Dodatkowe przykłady skryptów sieci interfejsu wiersza polecenia można znaleźć w [Azure Przegląd dokumentacji](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="50f61-137">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>