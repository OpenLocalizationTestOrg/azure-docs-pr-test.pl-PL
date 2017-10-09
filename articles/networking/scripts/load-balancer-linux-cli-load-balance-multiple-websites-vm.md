---
title: "Równoważenie obciążenia aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — wiele witryn sieci Web z wiersza polecenia platformy Azure hello | Dokumentacja firmy Microsoft"
description: "Równoważenie obciążenia Azure CLI przykładowym skrypcie — wiele witryn sieci Web toohello tej samej maszyny wirtualnej"
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 136da5d1783fb9f9dc87f1ffad8eec7b95c6bd7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="39087-103">Równoważenie obciążenia wielu witryn sieci Web</span><span class="sxs-lookup"><span data-stu-id="39087-103">Load balance multiple websites</span></span>

<span data-ttu-id="39087-104">Ten przykładowy skrypt tworzy sieć wirtualną z dwóch maszyn wirtualnych (VM), które są członkami zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="39087-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="39087-105">Moduł równoważenia obciążenia kieruje ruch na dwa oddzielne toohello dwóch maszyn wirtualnych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="39087-105">A load balancer directs traffic for two separate IP addresses toohello two VMs.</span></span> <span data-ttu-id="39087-106">Po uruchamianie skryptu hello można wdrożyć toohello oprogramowania serwera sieci web maszyn wirtualnych i obsługiwać wiele witryn sieci web z własnego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="39087-106">After running hello script, you could deploy web server software toohello VMs and host multiple web sites, each with its own IP address.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="39087-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="39087-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a><span data-ttu-id="39087-108">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="39087-108">Clean up deployment</span></span> 

<span data-ttu-id="39087-109">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="39087-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="39087-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="39087-110">Script explanation</span></span>

<span data-ttu-id="39087-111">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów sieci wirtualnej obciążenia równoważenia i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="39087-111">This script uses hello following commands toocreate a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="39087-112">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="39087-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="39087-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="39087-113">Command</span></span> | <span data-ttu-id="39087-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="39087-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="39087-115">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="39087-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="39087-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="39087-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="39087-117">Tworzenie sieci wirtualnej sieci az</span><span class="sxs-lookup"><span data-stu-id="39087-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="39087-118">Tworzy sieć wirtualna platformy Azure i podsieć.</span><span class="sxs-lookup"><span data-stu-id="39087-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="39087-119">Tworzenie sieci az publicznego ip</span><span class="sxs-lookup"><span data-stu-id="39087-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="39087-120">Tworzy publiczny adres IP z statyczny adres IP i skojarzonej nazwy DNS.</span><span class="sxs-lookup"><span data-stu-id="39087-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="39087-121">Utwórz równoważeniem obciążenia sieciowego az</span><span class="sxs-lookup"><span data-stu-id="39087-121">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="39087-122">Tworzy moduł równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="39087-122">Creates an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="39087-123">Utwórz sondowania równoważeniem obciążenia sieciowego az</span><span class="sxs-lookup"><span data-stu-id="39087-123">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="39087-124">Tworzy sondę modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="39087-124">Creates a load balancer probe.</span></span> <span data-ttu-id="39087-125">Sondę modułu równoważenia obciążenia jest używany toomonitor każdej maszyny Wirtualnej w zestawie usługi równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="39087-125">A load balancer probe is used toomonitor each VM in hello load balancer set.</span></span> <span data-ttu-id="39087-126">Jeśli żadnej maszyny Wirtualnej staje się niedostępny, ruch nie jest kierowany toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="39087-126">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="39087-127">Utwórz regułę równoważeniem obciążenia sieciowego az</span><span class="sxs-lookup"><span data-stu-id="39087-127">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="39087-128">Tworzy regułę modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="39087-128">Creates a load balancer rule.</span></span> <span data-ttu-id="39087-129">W tym przykładzie jest tworzona reguła dla portu 80.</span><span class="sxs-lookup"><span data-stu-id="39087-129">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="39087-130">Ruch HTTP dociera do usługi równoważenia obciążenia hello, jest kierowany tooport 80 jednej z maszyn wirtualnych hello w zestawie usługi równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="39087-130">As HTTP traffic arrives at hello load balancer, it is routed tooport 80 one of hello VMs in hello load balancer set.</span></span> |
| [<span data-ttu-id="39087-131">Utwórz az sieci lb-ip frontonu</span><span class="sxs-lookup"><span data-stu-id="39087-131">az network lb frontend-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | <span data-ttu-id="39087-132">Utwórz adres IP frontonu w hello modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="39087-132">Create a frontend IP address for hello Load Balancer.</span></span> |
| [<span data-ttu-id="39087-133">AZ lb puli adresów sieciowych — tworzenie</span><span class="sxs-lookup"><span data-stu-id="39087-133">az network lb address-pool create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | <span data-ttu-id="39087-134">Tworzy puli adresów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="39087-134">Creates a backend address pool.</span></span> |
| [<span data-ttu-id="39087-135">Utwórz az kart interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="39087-135">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="39087-136">Tworzy karty sieci wirtualnej i dołącza go toohello sieci wirtualnej i podsieci.</span><span class="sxs-lookup"><span data-stu-id="39087-136">Creates a virtual network card and attaches it toohello virtual network, and subnet.</span></span> |
| [<span data-ttu-id="39087-137">Tworzenie maszyny wirtualnej az zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="39087-137">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="39087-138">Tworzy zestaw dostępności.</span><span class="sxs-lookup"><span data-stu-id="39087-138">Creates an availability set.</span></span> <span data-ttu-id="39087-139">Zestawy dostępności upewnij się, czas działania aplikacji poprzez rozłożenie zasobów fizycznych hello maszyny wirtualnej tak, aby w przypadku niepowodzenia hello cały zestaw nie jest wykonywane.</span><span class="sxs-lookup"><span data-stu-id="39087-139">Availability sets ensure application uptime by spreading hello virtual machines across physical resources such that if failure occurs, hello entire set is not effected.</span></span> |
| [<span data-ttu-id="39087-140">Tworzenie kart sieciowych az ip-config</span><span class="sxs-lookup"><span data-stu-id="39087-140">az network nic ip-config create</span></span>](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | <span data-ttu-id="39087-141">Tworzy confiuration IP.</span><span class="sxs-lookup"><span data-stu-id="39087-141">Creates an IP confiuration.</span></span> <span data-ttu-id="39087-142">Musi mieć hello Microsoft.Network/AllowMultipleIpConfigurationsPerNic funkcja jest włączona dla Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="39087-142">You must have hello Microsoft.Network/AllowMultipleIpConfigurationsPerNic feature enabled for your subscription.</span></span> <span data-ttu-id="39087-143">Tylko jedną konfigurację mogą być oznaczone jako hello podstawową konfigurację protokołu IP dla karty Sieciowej, za pomocą hello — flagi podstawowej upewnij.</span><span class="sxs-lookup"><span data-stu-id="39087-143">Only one configuration may be designated as hello primary IP configuration per NIC, using hello --make-primary flag.</span></span> |
| [<span data-ttu-id="39087-144">Tworzenie maszyny wirtualnej az</span><span class="sxs-lookup"><span data-stu-id="39087-144">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="39087-145">Tworzy maszynę wirtualną hello i łączy go toohello karty sieciowej, sieć wirtualną, podsieci i NSG.</span><span class="sxs-lookup"><span data-stu-id="39087-145">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="39087-146">To polecenie określa również toobe obrazu maszyny wirtualnej hello używane i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="39087-146">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="39087-147">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="39087-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="39087-148">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="39087-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="39087-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="39087-149">Next steps</span></span>

<span data-ttu-id="39087-150">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="39087-150">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="39087-151">Dodatkowe przykłady skryptów sieci interfejsu wiersza polecenia można znaleźć w hello [Azure Przegląd dokumentacji](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="39087-151">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
