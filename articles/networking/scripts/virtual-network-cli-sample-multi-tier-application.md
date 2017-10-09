---
title: "aaaAzure interfejsu wiersza polecenia skryptu przykładowe — tworzenie sieci dla aplikacji wielowarstwowych | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: deeb3f459499cebd1b8ded6a299eb759d49cf08d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="d1f3a-103">Tworzenie sieci dla aplikacji wielowarstwowych</span><span class="sxs-lookup"><span data-stu-id="d1f3a-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="d1f3a-104">Ten przykładowy skrypt tworzy sieć wirtualną z podsieci frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="d1f3a-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="d1f3a-105">Podsieci frontonu toohello ruchu jest ograniczony tooHTTP i SSH, podczas toohello ruchu podsieci wewnętrznej jest ograniczona tooMySQL, port 3306.</span><span class="sxs-lookup"><span data-stu-id="d1f3a-105">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> <span data-ttu-id="d1f3a-106">Po uruchamianie skryptu hello masz dwie maszyny wirtualne, w każdej podsieci, którą można wdrożyć serwera sieci web i MySQL oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="d1f3a-106">After running hello script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="d1f3a-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="d1f3a-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d1f3a-108">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="d1f3a-108">Clean up deployment</span></span> 

<span data-ttu-id="d1f3a-109">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="d1f3a-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="d1f3a-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="d1f3a-110">Script explanation</span></span>

<span data-ttu-id="d1f3a-111">Ten skrypt używa powitania po toocreate poleceń, grupy zasobów, sieci wirtualnej i grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="d1f3a-111">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="d1f3a-112">Każde polecenie w dokumentacji konkretnego toocommand łącza tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="d1f3a-112">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="d1f3a-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="d1f3a-113">Command</span></span> | <span data-ttu-id="d1f3a-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d1f3a-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d1f3a-115">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="d1f3a-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="d1f3a-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="d1f3a-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d1f3a-117">Tworzenie sieci wirtualnej sieci az</span><span class="sxs-lookup"><span data-stu-id="d1f3a-117">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="d1f3a-118">Tworzy sieć wirtualna platformy Azure i podsieci frontonu.</span><span class="sxs-lookup"><span data-stu-id="d1f3a-118">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="d1f3a-119">Utwórz podsieć sieci az</span><span class="sxs-lookup"><span data-stu-id="d1f3a-119">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="d1f3a-120">Tworzy podsieć zaplecza.</span><span class="sxs-lookup"><span data-stu-id="d1f3a-120">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="d1f3a-121">Tworzenie sieci az publicznego ip</span><span class="sxs-lookup"><span data-stu-id="d1f3a-121">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="d1f3a-122">Tworzy publicznego adresu IP adres tooaccess hello maszyny Wirtualnej na podstawie hello Internet.</span><span class="sxs-lookup"><span data-stu-id="d1f3a-122">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="d1f3a-123">Utwórz az kart interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="d1f3a-123">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="d1f3a-124">Tworzy interfejsy sieci wirtualnej i dołącza je podsieci sieci wirtualnej toohello frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="d1f3a-124">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="d1f3a-125">Tworzenie grupy nsg sieci az</span><span class="sxs-lookup"><span data-stu-id="d1f3a-125">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="d1f3a-126">Tworzy grupy zabezpieczeń sieci (NSG), które są skojarzone toohello podsieci frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="d1f3a-126">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="d1f3a-127">Tworzenie reguły nsg sieci az</span><span class="sxs-lookup"><span data-stu-id="d1f3a-127">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="d1f3a-128">Tworzy reguły NSG, które zezwala lub blokuje określone porty toospecific podsieci.</span><span class="sxs-lookup"><span data-stu-id="d1f3a-128">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="d1f3a-129">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="d1f3a-129">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="d1f3a-130">Tworzy maszyny wirtualne i dołącza tooeach karty Sieciowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d1f3a-130">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="d1f3a-131">To polecenie określa również toouse obrazu maszyny wirtualnej hello i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="d1f3a-131">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="d1f3a-132">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="d1f3a-132">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="d1f3a-133">Usuwa grupę zasobów i wszystkie zasoby, które zawiera.</span><span class="sxs-lookup"><span data-stu-id="d1f3a-133">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d1f3a-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d1f3a-134">Next steps</span></span>

<span data-ttu-id="d1f3a-135">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d1f3a-135">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="d1f3a-136">Dodatkowe przykłady skryptów sieci interfejsu wiersza polecenia można znaleźć w hello [Azure Przegląd dokumentacji](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="d1f3a-136">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
