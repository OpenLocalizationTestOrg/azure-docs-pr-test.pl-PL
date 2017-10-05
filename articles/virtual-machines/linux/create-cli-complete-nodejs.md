---
title: "Utwórz pełną środowiska Linux z interfejsu wiersza polecenia platformy Azure w wersji 1.0 | Dokumentacja firmy Microsoft"
description: "Tworzenie magazynu, Maszynę wirtualną systemu Linux, sieci wirtualnej i podsieci, usługi równoważenia obciążenia, karty Sieciowej, publicznego adresu IP i sieciową grupę zabezpieczeń, wszystkie od podstaw przy użyciu 1.0 interfejsu wiersza polecenia platformy Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 201ccd523e49d638ace50fbc0ffdceb705b35473
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-complete-linux-environment-with-the-azure-cli-10"></a><span data-ttu-id="9e4a1-103">Utwórz pełną środowiska Linux z interfejsu wiersza polecenia platformy Azure w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="9e4a1-103">Create a complete Linux environment with the Azure CLI 1.0</span></span>
<span data-ttu-id="9e4a1-104">W tym artykule budujemy prosta sieć z modułem równoważenia obciążenia i para maszyn wirtualnych, które są przydatne w przypadku tworzenia i przetwarzania proste.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-104">In this article, we build a simple network with a load balancer and a pair of VMs that are useful for development and simple computing.</span></span> <span data-ttu-id="9e4a1-105">Firma Microsoft przeprowadzenie procesu polecenie, dopóki nie uzyskasz dwóch pracy, bezpieczne maszyn wirtualnych systemu Linux których możesz połączyć z dowolnego miejsca w Internecie.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-105">We walk through the process command by command, until you have two working, secure Linux VMs to which you can connect from anywhere on the Internet.</span></span> <span data-ttu-id="9e4a1-106">Następnie możesz przejść do bardziej złożone sieci i środowiskach.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-106">Then you can move on to more complex networks and environments.</span></span>

<span data-ttu-id="9e4a1-107">Przeglądania zapoznanie się z hierarchią zależności modelu wdrażania usługi Resource Manager umożliwia, czy o ile włączenie go zawiera.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-107">Along the way, you learn about the dependency hierarchy that the Resource Manager deployment model gives you, and about how much power it provides.</span></span> <span data-ttu-id="9e4a1-108">Po jak system jest oparty, można go znacznie szybciej odtworzyć za pomocą [szablonów usługi Azure Resource Manager](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e4a1-108">After you see how the system is built, you can rebuild it much more quickly by using [Azure Resource Manager templates](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="9e4a1-109">Ponadto po dowiesz się, jak części środowiska dopasowania, tworzenie szablonów można zautomatyzować je staje się łatwiejsze.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-109">Also, after you learn how the parts of your environment fit together, creating templates to automate them becomes easier.</span></span>

<span data-ttu-id="9e4a1-110">Środowisko zawiera:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-110">The environment contains:</span></span>

* <span data-ttu-id="9e4a1-111">Dwie maszyny wirtualne w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-111">Two VMs inside an availability set.</span></span>
* <span data-ttu-id="9e4a1-112">Usługi równoważenia obciążenia z regułą równoważenia obciążenia na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-112">A load balancer with a load-balancing rule on port 80.</span></span>
* <span data-ttu-id="9e4a1-113">Zasady zabezpieczeń grupy (NSG) ochrony maszyny Wirtualnej niepożądanego ruchu w sieci.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-113">Network security group (NSG) rules to protect your VM from unwanted traffic.</span></span>

<span data-ttu-id="9e4a1-114">Aby utworzyć niestandardowe środowisko, należy najnowszej [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) w trybie Menedżera zasobów (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="9e4a1-114">To create this custom environment, you need the latest [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in Resource Manager mode (`azure config mode arm`).</span></span> <span data-ttu-id="9e4a1-115">Należy również JSON, narzędzie do analizy.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-115">You also need a JSON parsing tool.</span></span> <span data-ttu-id="9e4a1-116">W tym przykładzie użyto [jq](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="9e4a1-116">This example uses [jq](https://stedolan.github.io/jq/).</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="9e4a1-117">Wersje interfejsu wiersza polecenia umożliwiające wykonanie zadania</span><span class="sxs-lookup"><span data-stu-id="9e4a1-117">CLI versions to complete the task</span></span>
<span data-ttu-id="9e4a1-118">Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-118">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="9e4a1-119">[Azure CLI 1.0](#quick-commands) — nasze interfejsu wiersza polecenia dla klasycznego i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="9e4a1-119">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="9e4a1-120">[Interfejs wiersza polecenia platformy Azure w wersji 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) — nasz interfejs wiersza polecenia nowej generacji dla modelu wdrażania na potrzeby zarządzania zasobami</span><span class="sxs-lookup"><span data-stu-id="9e4a1-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="9e4a1-121">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="9e4a1-121">Quick commands</span></span>
<span data-ttu-id="9e4a1-122">Jeśli chcesz szybko wykonać zadanie, następujące szczegóły sekcji bazie polecenia do przekazania Maszynę wirtualną na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-122">If you need to quickly accomplish the task, the following section details the base commands to upload a VM to Azure.</span></span> <span data-ttu-id="9e4a1-123">Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć w pozostałej części dokumentu, początkowa [tutaj](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="9e4a1-123">More detailed information and context for each step can be found in the rest of the document, starting [here](#detailed-walkthrough).</span></span>

<span data-ttu-id="9e4a1-124">Upewnij się, że masz [1.0 interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) zalogowany i w trybie Menedżera zasobów:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-124">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="9e4a1-125">W poniższych przykładach Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-125">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="9e4a1-126">Przykład nazwy parametru zawierają `myResourceGroup`, `mystorageaccount`, i `myVM`.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-126">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

<span data-ttu-id="9e4a1-127">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-127">Create the resource group.</span></span> <span data-ttu-id="9e4a1-128">Poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w `westeurope` lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-128">The following example creates a resource group named `myResourceGroup` in the `westeurope` location:</span></span>

```azurecli
azure group create -n myResourceGroup -l westeurope
```

<span data-ttu-id="9e4a1-129">Sprawdź grupy zasobów, przy użyciu analizatora składni JSON:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-129">Verify the resource group by using the JSON parser:</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="9e4a1-130">Tworzenie konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-130">Create the storage account.</span></span> <span data-ttu-id="9e4a1-131">Poniższy przykład tworzy konto magazynu o nazwie `mystorageaccount`.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-131">The following example creates a storage account named `mystorageaccount`.</span></span> <span data-ttu-id="9e4a1-132">(Nazwa konta magazynu musi być unikatowa, aby podać własną unikatową nazwę.)</span><span class="sxs-lookup"><span data-stu-id="9e4a1-132">(The storage account name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

<span data-ttu-id="9e4a1-133">Sprawdź konto magazynu przy użyciu analizatora składni JSON:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-133">Verify the storage account by using the JSON parser:</span></span>

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

<span data-ttu-id="9e4a1-134">Utwórz sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-134">Create the virtual network.</span></span> <span data-ttu-id="9e4a1-135">Poniższy przykład tworzy sieć wirtualną o nazwie `myVnet`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-135">The following example creates a virtual network named `myVnet`:</span></span>

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

<span data-ttu-id="9e4a1-136">Utwórz podsieć.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-136">Create a subnet.</span></span> <span data-ttu-id="9e4a1-137">Poniższy przykład tworzy podsieć o nazwie `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-137">The following example creates a subnet named `mySubnet`:</span></span>

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

<span data-ttu-id="9e4a1-138">Sprawdź sieć wirtualna i podsieć, za pomocą analizatora składni JSON:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-138">Verify the virtual network and subnet by using the JSON parser:</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="9e4a1-139">Tworzenie publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-139">Create a public IP.</span></span> <span data-ttu-id="9e4a1-140">Poniższy przykład tworzy publicznego adresu IP o nazwie `myPublicIP` o nazwie DNS `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-140">The following example creates a public IP named `myPublicIP` with the DNS name of `mypublicdns`.</span></span> <span data-ttu-id="9e4a1-141">(Nazwa DNS musi być unikatowa, aby podać własną unikatową nazwę.)</span><span class="sxs-lookup"><span data-stu-id="9e4a1-141">(The DNS name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

<span data-ttu-id="9e4a1-142">Tworzenie usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-142">Create the load balancer.</span></span> <span data-ttu-id="9e4a1-143">Poniższy przykład tworzy moduł równoważenia obciążenia o nazwie `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-143">The following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

<span data-ttu-id="9e4a1-144">Utwórz pulę IP frontonu dla usługi równoważenia obciążenia i skojarz publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-144">Create a front-end IP pool for the load balancer, and associate the public IP.</span></span> <span data-ttu-id="9e4a1-145">Poniższy przykład tworzy frontonu pula IP o nazwie `mySubnetPool`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-145">The following example creates a front-end IP pool named `mySubnetPool`:</span></span>

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

<span data-ttu-id="9e4a1-146">Tworzenie puli adresów IP zaplecza dla usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-146">Create the back-end IP pool for the load balancer.</span></span> <span data-ttu-id="9e4a1-147">Poniższy przykład tworzy pula IP zaplecza, o nazwie `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-147">The following example creates a back-end IP pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

<span data-ttu-id="9e4a1-148">Utwórz sieć dla ruchu przychodzącego SSH reguły translacji adresów adres usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-148">Create SSH inbound network address translation (NAT) rules for the load balancer.</span></span> <span data-ttu-id="9e4a1-149">Poniższy przykład tworzy dwie reguły modułu równoważenia obciążenia, `myLoadBalancerRuleSSH1` i `myLoadBalancerRuleSSH2`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-149">The following example creates two load balancer rules, `myLoadBalancerRuleSSH1` and `myLoadBalancerRuleSSH2`:</span></span>

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

<span data-ttu-id="9e4a1-150">Utwórz sieć web przychodzącej reguły NAT modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-150">Create the web inbound NAT rules for the load balancer.</span></span> <span data-ttu-id="9e4a1-151">Poniższy przykład tworzy regułę równoważenia obciążenia o nazwie `myLoadBalancerRuleWeb`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-151">The following example creates a load balancer rule named `myLoadBalancerRuleWeb`:</span></span>

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

<span data-ttu-id="9e4a1-152">Utwórz sondy kondycji modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-152">Create the load balancer health probe.</span></span> <span data-ttu-id="9e4a1-153">Poniższy przykład tworzy sondowaniem TCP o nazwie `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-153">The following example creates a TCP probe named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

<span data-ttu-id="9e4a1-154">Sprawdź usługi równoważenia obciążenia, pule adresów IP i reguł NAT, za pomocą analizatora składni JSON:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-154">Verify the load balancer, IP pools, and NAT rules by using the JSON parser:</span></span>

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

<span data-ttu-id="9e4a1-155">Tworzenie pierwszej karty interfejsu sieciowego (NIC).</span><span class="sxs-lookup"><span data-stu-id="9e4a1-155">Create the first network interface card (NIC).</span></span> <span data-ttu-id="9e4a1-156">Zastąp `#####-###-###` sekcje z identyfikatorem subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9e4a1-156">Replace the `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="9e4a1-157">Identyfikator jest odnotowany w danych wyjściowych subskrypcji **jq** podczas badania tworzysz zasoby.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-157">Your subscription ID is noted in the output of **jq** when you examine the resources you are creating.</span></span> <span data-ttu-id="9e4a1-158">Można również wyświetlić identyfikator subskrypcji z `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-158">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="9e4a1-159">Poniższy przykład tworzy karty Sieciowej o nazwie `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-159">The following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

<span data-ttu-id="9e4a1-160">Tworzenie drugiej karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-160">Create the second NIC.</span></span> <span data-ttu-id="9e4a1-161">Poniższy przykład tworzy karty Sieciowej o nazwie `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-161">The following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

<span data-ttu-id="9e4a1-162">Sprawdź dwie karty sieciowe za pomocą analizatora składni JSON:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-162">Verify the two NICs by using the JSON parser:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

<span data-ttu-id="9e4a1-163">Utwórz grupę zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-163">Create the network security group.</span></span> <span data-ttu-id="9e4a1-164">Poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-164">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

<span data-ttu-id="9e4a1-165">Dodaj dwie reguły ruchu przychodzącego dla grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-165">Add two inbound rules for the network security group.</span></span> <span data-ttu-id="9e4a1-166">Poniższy przykład tworzy dwie reguły `myNetworkSecurityGroupRuleSSH` i `myNetworkSecurityGroupRuleHTTP`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-166">The following example creates two rules, `myNetworkSecurityGroupRuleSSH` and `myNetworkSecurityGroupRuleHTTP`:</span></span>

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

<span data-ttu-id="9e4a1-167">Sprawdź grupy zabezpieczeń sieci i reguł ruchu przychodzącego, za pomocą analizatora składni JSON:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-167">Verify the network security group and inbound rules by using the JSON parser:</span></span>

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

<span data-ttu-id="9e4a1-168">Powiąż sieciową grupę zabezpieczeń z dwiema kartami sieciowymi:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-168">Bind the network security group to the two NICs:</span></span>

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

<span data-ttu-id="9e4a1-169">Tworzenie zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-169">Create the availability set.</span></span> <span data-ttu-id="9e4a1-170">Poniższy przykład tworzy zbiór nazwanego dostępności `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-170">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

<span data-ttu-id="9e4a1-171">Tworzenie pierwszej maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-171">Create the first Linux VM.</span></span> <span data-ttu-id="9e4a1-172">Poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM1`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-172">The following example creates a VM named `myVM1`:</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM1 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic1 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="9e4a1-173">Tworzenie drugiej maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-173">Create the second Linux VM.</span></span> <span data-ttu-id="9e4a1-174">Poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM2`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-174">The following example creates a VM named `myVM2`:</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM2 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic2 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="9e4a1-175">Użyj analizatora składni JSON do sprawdzenia, czy wszystko, który został utworzony:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-175">Use the JSON parser to verify that everything that was built:</span></span>

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

<span data-ttu-id="9e4a1-176">Wyeksportuj nowe środowisko do szablonu w celu szybkiego ponownego tworzenia nowych wystąpień:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-176">Export your new environment to a template to quickly re-create new instances:</span></span>

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="9e4a1-177">Szczegółowy przewodnik</span><span class="sxs-lookup"><span data-stu-id="9e4a1-177">Detailed walkthrough</span></span>
<span data-ttu-id="9e4a1-178">Szczegółowy opis kroków, które należy wykonać wyjaśnić, każdego polecenia czynności podczas tworzenia Twoje środowisko.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-178">The detailed steps that follow explain what each command is doing as you build out your environment.</span></span> <span data-ttu-id="9e4a1-179">Te pojęcia są przydatne podczas tworzenia własnego niestandardowego środowiska dla rozwoju lub produkcji.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-179">These concepts are helpful when you build your own custom environments for development or production.</span></span>

<span data-ttu-id="9e4a1-180">Upewnij się, że masz [1.0 interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) zalogowany i w trybie Menedżera zasobów:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-180">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="9e4a1-181">W poniższych przykładach Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-181">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="9e4a1-182">Przykład nazwy parametru zawierają `myResourceGroup`, `mystorageaccount`, i `myVM`.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-182">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

## <a name="create-resource-groups-and-choose-deployment-locations"></a><span data-ttu-id="9e4a1-183">Tworzenie grupy zasobów, a następnie wybierz pozycję lokalizacji wdrożenia</span><span class="sxs-lookup"><span data-stu-id="9e4a1-183">Create resource groups and choose deployment locations</span></span>
<span data-ttu-id="9e4a1-184">Grupy zasobów platformy Azure są jednostki wdrażania, które zawierają informacje o konfiguracji i metadanych, aby umożliwić zarządzanie logicznej wdrożenia zasobów.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-184">Azure resource groups are logical deployment entities that contain configuration information and metadata to enable the logical management of resource deployments.</span></span> <span data-ttu-id="9e4a1-185">Poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w `westeurope` lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-185">The following example creates a resource group named `myResourceGroup` in the `westeurope` location:</span></span>

```azurecli
azure group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="9e4a1-186">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-186">Output:</span></span>

```azurecli                        
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westeurope
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

## <a name="create-a-storage-account"></a><span data-ttu-id="9e4a1-187">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="9e4a1-187">Create a storage account</span></span>
<span data-ttu-id="9e4a1-188">Należy korzystać z kont magazynu dla dysków maszyny Wirtualnej i dla wszystkich dysków dodatkowe dane, które chcesz dodać.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-188">You need storage accounts for your VM disks and for any additional data disks that you want to add.</span></span> <span data-ttu-id="9e4a1-189">Możesz utworzyć konta magazynu prawie natychmiast po utworzeniu grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-189">You create storage accounts almost immediately after you create resource groups.</span></span>

<span data-ttu-id="9e4a1-190">W tym miejscu użyjemy `azure storage account create` polecenia przekazywanie Lokalizacja konta, grupy zasobów, która kontroluje, a typ obsługi magazynu ma.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-190">Here we use the `azure storage account create` command, passing the location of the account, the resource group that controls it, and the type of storage support you want.</span></span> <span data-ttu-id="9e4a1-191">Poniższy przykład tworzy konto magazynu o nazwie `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-191">The following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

<span data-ttu-id="9e4a1-192">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-192">Output:</span></span>

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

<span data-ttu-id="9e4a1-193">Do sprawdzenia naszej grupy zasobów za pomocą `azure group show` polecenia, można użyć [jq](https://stedolan.github.io/jq/) narzędzia wraz z programem `--json` opcji wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-193">To examine our resource group by using the `azure group show` command, let's use the [jq](https://stedolan.github.io/jq/) tool along with the `--json` Azure CLI option.</span></span> <span data-ttu-id="9e4a1-194">(Można użyć **jsawk** lub żadnej biblioteki języka aby przeanalizować dane JSON.)</span><span class="sxs-lookup"><span data-stu-id="9e4a1-194">(You can use **jsawk** or any language library you prefer to parse the JSON.)</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="9e4a1-195">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-195">Output:</span></span>

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

<span data-ttu-id="9e4a1-196">Do sprawdzania, czy konto magazynu przy użyciu interfejsu wiersza polecenia, należy najpierw ustawić nazwy kont i kluczy.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-196">To investigate the storage account by using the CLI, you first need to set the account names and keys.</span></span> <span data-ttu-id="9e4a1-197">Zastąp nazwę, która zostanie wybrana nazwa konta magazynu w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-197">Replace the name of the storage account in the following example with a name that you choose:</span></span>

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

<span data-ttu-id="9e4a1-198">Następnie można wyświetlić informacje o pamięci masowej łatwo:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-198">Then you can view your storage information easily:</span></span>

```azurecli
azure storage container list
```

<span data-ttu-id="9e4a1-199">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-199">Output:</span></span>

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="9e4a1-200">Tworzenie sieci wirtualnej i podsieci</span><span class="sxs-lookup"><span data-stu-id="9e4a1-200">Create a virtual network and subnet</span></span>
<span data-ttu-id="9e4a1-201">Następnie możesz zacząć należy utworzyć sieć wirtualną z systemem Azure i podsieć, w którym można utworzyć maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-201">Next you're going to need to create a virtual network running in Azure and a subnet in which you can create your VMs.</span></span> <span data-ttu-id="9e4a1-202">Poniższy przykład tworzy sieć wirtualną o nazwie `myVnet` z `192.168.0.0/16` prefiks adresu:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-202">The following example creates a virtual network named `myVnet` with the `192.168.0.0/16` address prefix:</span></span>

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="9e4a1-203">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-203">Output:</span></span>

```azurecli
info:    Executing command network vnet create
+ Looking up virtual network "myVnet"
+ Creating virtual network "myVnet"
+ Loading virtual network state
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet
data:    Name                            : myVnet
data:    Type                            : Microsoft.Network/virtualNetworks
data:    Location                        : westeurope
data:    ProvisioningState               : Succeeded
data:    Address prefixes:
data:      192.168.0.0/16
info:    network vnet create command OK
```

<span data-ttu-id="9e4a1-204">Ponownie, możemy użyć opcji--json `azure group show` i `jq` aby zobaczyć, jak tworzymy naszych zasobów.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-204">Again, let's use the --json option of `azure group show` and `jq` to see how we're building our resources.</span></span> <span data-ttu-id="9e4a1-205">Teraz `storageAccounts` zasobów i `virtualNetworks` zasobów.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-205">We now have a `storageAccounts` resource and a `virtualNetworks` resource.</span></span>  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="9e4a1-206">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-206">Output:</span></span>

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
      "name": "myVnet",
      "type": "virtualNetworks",
      "location": "westeurope",
      "tags": null
    },
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

<span data-ttu-id="9e4a1-207">Teraz Utwórzmy podsieci `myVnet` sieci wirtualnej, w której maszyny wirtualne są wdrażane.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-207">Now let's create a subnet in the `myVnet` virtual network into which the VMs are deployed.</span></span> <span data-ttu-id="9e4a1-208">Używamy `azure network vnet subnet create` polecenia wraz z zasobów już utworzyliśmy: `myResourceGroup` grupy zasobów i `myVnet` sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-208">We use the `azure network vnet subnet create` command, along with the resources we've already created: the `myResourceGroup` resource group and the `myVnet` virtual network.</span></span> <span data-ttu-id="9e4a1-209">W poniższym przykładzie dodamy podsieci o nazwie `mySubnet` z prefiksem adresu podsieci `192.168.1.0/24`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-209">In the following example, we add the subnet named `mySubnet` with the subnet address prefix of `192.168.1.0/24`:</span></span>

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

<span data-ttu-id="9e4a1-210">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-210">Output:</span></span>

```azurecli
info:    Executing command network vnet subnet create
+ Looking up the subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up the subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

<span data-ttu-id="9e4a1-211">Ponieważ podsieci logicznie znajduje się w sieci wirtualnej, firma Microsoft poszukaj informacji o podsieci za pomocą polecenia nieco inne.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-211">Because the subnet is logically inside the virtual network, we look for the subnet information with a slightly different command.</span></span> <span data-ttu-id="9e4a1-212">Polecenie używamy jest `azure network vnet show`, ale w dalszym ciągu Sprawdź dane wyjściowe JSON przy użyciu `jq`.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-212">The command we use is `azure network vnet show`, but we continue to examine the JSON output by using `jq`.</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="9e4a1-213">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-213">Output:</span></span>

```json
{
  "subnets": [
    {
      "ipConfigurations": [],
      "addressPrefix": "192.168.1.0/24",
      "provisioningState": "Succeeded",
      "name": "mySubnet",
      "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
    }
  ],
  "tags": {},
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "provisioningState": "Succeeded",
  "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "name": "myVnet",
  "location": "westeurope"
}
```

## <a name="create-a-public-ip-address"></a><span data-ttu-id="9e4a1-214">Tworzenie publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="9e4a1-214">Create a public IP address</span></span>
<span data-ttu-id="9e4a1-215">Teraz Utwórzmy publicznego adresu IP (PIP), na który mamy przypisywać przez moduł równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-215">Now let's create the public IP address (PIP) that we assign to your load balancer.</span></span> <span data-ttu-id="9e4a1-216">Umożliwia łączenie się z maszyn wirtualnych z Internetu przy użyciu `azure network public-ip create` polecenia.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-216">It enables you to connect to your VMs from the Internet by using the `azure network public-ip create` command.</span></span> <span data-ttu-id="9e4a1-217">Ponieważ domyślnym adresem jest dynamiczny, utworzymy nazwanego wpisu DNS w **cloudapp.azure.com** domeny przy użyciu `--domain-name-label` opcji.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-217">Because the default address is dynamic, we create a named DNS entry in the **cloudapp.azure.com** domain by using the `--domain-name-label` option.</span></span> <span data-ttu-id="9e4a1-218">Poniższy przykład tworzy publicznego adresu IP o nazwie `myPublicIP` o nazwie DNS `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-218">The following example creates a public IP named `myPublicIP` with the DNS name of `mypublicdns`.</span></span> <span data-ttu-id="9e4a1-219">Nazwa DNS musi być unikatowa, należy dostarczyć własną unikatową nazwę DNS:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-219">Because the DNS name must be unique, you provide your own unique DNS name:</span></span>

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

<span data-ttu-id="9e4a1-220">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-220">Output:</span></span>

```azurecli
info:    Executing command network public-ip create
+ Looking up the public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up the public ip "myPublicIP"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
data:    Name                            : myPublicIP
data:    Type                            : Microsoft.Network/publicIPAddresses
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Allocation method               : Dynamic
data:    Idle timeout                    : 4
data:    Domain name label               : mypublicdns
data:    FQDN                            : mypublicdns.westeurope.cloudapp.azure.com
info:    network public-ip create command OK
```

<span data-ttu-id="9e4a1-221">Publiczny adres IP jest również zasobem najwyższego poziomu, tak aby było widać, z `azure group show`.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-221">The public IP address is also a top-level resource, so you can see it with `azure group show`.</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="9e4a1-222">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-222">Output:</span></span>

```json
{
"tags": {},
"id": "/subscriptions/guid/resourceGroups/myResourceGroup",
"name": "myResourceGroup",
"provisioningState": "Succeeded",
"location": "westeurope",
"properties": {
    "provisioningState": "Succeeded"
},
"resources": [
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "name": "myPublicIP",
    "type": "publicIPAddresses",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
    "name": "myVnet",
    "type": "virtualNetworks",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
    "name": "mystorageaccount",
    "type": "storageAccounts",
    "location": "westeurope",
    "tags": null
    }
],
"permissions": [
    {
    "actions": [
        "*"
    ],
    "notActions": []
    }
]
}
```

<span data-ttu-id="9e4a1-223">Możesz przejrzeć szczegółowe zasobów, włącznie z w pełni kwalifikowaną nazwę (FQDN) domeny podrzędnej, korzystając z pełną `azure network public-ip show` polecenia.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-223">You can investigate more resource details, including the fully qualified domain name (FQDN) of the subdomain, by using the complete `azure network public-ip show` command.</span></span> <span data-ttu-id="9e4a1-224">Została przydzielona logicznie zasobu publicznego adresu IP, ale nie został jeszcze przypisany określony adres.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-224">The public IP address resource has been allocated logically, but a specific address has not yet been assigned.</span></span> <span data-ttu-id="9e4a1-225">Aby uzyskać adres IP, możesz zacząć wymagają modułu równoważenia obciążenia, które firma Microsoft nie został jeszcze utworzony.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-225">To obtain an IP address, you're going to need a load balancer, which we have not yet created.</span></span>

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

<span data-ttu-id="9e4a1-226">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-226">Output:</span></span>

```json
{
"tags": {},
"publicIpAllocationMethod": "Dynamic",
"dnsSettings": {
    "domainNameLabel": "mypublicdns",
    "fqdn": "mypublicdns.westeurope.cloudapp.azure.com"
},
"idleTimeoutInMinutes": 4,
"provisioningState": "Succeeded",
"etag": "W/\"c63154b3-1130-49b9-a887-877d74d5ebc5\"",
"id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
"name": "myPublicIP",
"location": "westeurope"
}
```

## <a name="create-a-load-balancer-and-ip-pools"></a><span data-ttu-id="9e4a1-227">Tworzenie modułu równoważenia obciążenia i pule adresów IP</span><span class="sxs-lookup"><span data-stu-id="9e4a1-227">Create a load balancer and IP pools</span></span>
<span data-ttu-id="9e4a1-228">Podczas tworzenia modułu równoważenia obciążenia, umożliwia rozłożenie ruchu między wieloma maszynami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-228">When you create a load balancer, it enables you to distribute traffic across multiple VMs.</span></span> <span data-ttu-id="9e4a1-229">Umożliwia także nadmiarowości aplikacji, uruchamiając wiele maszyn wirtualnych, które odpowiadają na żądania użytkownika w przypadku obsługi lub dużym obciążeniem.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-229">It also provides redundancy to your application by running multiple VMs that respond to user requests in the event of maintenance or heavy loads.</span></span> <span data-ttu-id="9e4a1-230">Poniższy przykład tworzy moduł równoważenia obciążenia o nazwie `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-230">The following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

<span data-ttu-id="9e4a1-231">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-231">Output:</span></span>

```azurecli
info:    Executing command network lb create
+ Looking up the load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

<span data-ttu-id="9e4a1-232">Naszej usługi równoważenia obciążenia jest dość pusty, więc warto utworzyć niektóre pule adresów IP.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-232">Our load balancer is fairly empty, so let's create some IP pools.</span></span> <span data-ttu-id="9e4a1-233">Chcemy, aby utworzyć dwie pule IP naszej usługi równoważenia obciążenia, jeden dla frontonu i jeden dla wewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-233">We want to create two IP pools for our load balancer, one for the front end and one for the back end.</span></span> <span data-ttu-id="9e4a1-234">Puli adresów IP frontonu jest publicznie widoczna.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-234">The front-end IP pool is publicly visible.</span></span> <span data-ttu-id="9e4a1-235">Istnieje również lokalizacji, do którego możemy przypisać PIP, który utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-235">It's also the location to which we assign the PIP that we created earlier.</span></span> <span data-ttu-id="9e4a1-236">Następnie używamy puli zaplecza jako lokalizacji dla naszej maszyn wirtualnych do nawiązania połączenia.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-236">Then we use the back-end pool as a location for our VMs to connect to.</span></span> <span data-ttu-id="9e4a1-237">W ten sposób przepływ ruchu za pośrednictwem usługi równoważenia obciążenia do maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-237">That way, the traffic can flow through the load balancer to the VMs.</span></span>

<span data-ttu-id="9e4a1-238">Najpierw utwórz naszych frontonu puli adresów IP.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-238">First, let's create our front-end IP pool.</span></span> <span data-ttu-id="9e4a1-239">Poniższy przykład tworzy puli frontonu o nazwie `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-239">The following example creates a front-end pool named `myFrontEndPool`:</span></span>

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

<span data-ttu-id="9e4a1-240">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-240">Output:</span></span>

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up the load balancer "myLoadBalancer"
+ Looking up the public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

<span data-ttu-id="9e4a1-241">Należy zwrócić uwagę, jak użyliśmy `--public-ip-name` przełącznik, aby przekazać `myPublicIP` utworzonej wcześniej.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-241">Note how we used the `--public-ip-name` switch to pass in the `myPublicIP` that we created earlier.</span></span> <span data-ttu-id="9e4a1-242">Przypisywanie publicznego adresu IP do modułu równoważenia obciążenia można osiągnąć maszyn wirtualnych przez Internet.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-242">Assigning the public IP address to the load balancer allows you to reach your VMs across the Internet.</span></span>

<span data-ttu-id="9e4a1-243">Następnie Utwórzmy naszych drugi pula IP teraz naszych ruchu zaplecza.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-243">Next, let's create our second IP pool, this time for our back-end traffic.</span></span> <span data-ttu-id="9e4a1-244">Poniższy przykład tworzy puli zaplecza, o nazwie `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-244">The following example creates a back-end pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

<span data-ttu-id="9e4a1-245">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-245">Output:</span></span>

```azurecli
info:    Executing command network lb address-pool create
+ Looking up the load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

<span data-ttu-id="9e4a1-246">Zobaczysz, jak robi naszej usługi równoważenia obciążenia przez wyszukiwanie z `azure network lb show` i badanie danych wyjściowych JSON:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-246">We can see how our load balancer is doing by looking with `azure network lb show` and examining the JSON output:</span></span>

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

<span data-ttu-id="9e4a1-247">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-247">Output:</span></span>

```json
{
  "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [],
  "probes": []
}
```

## <a name="create-load-balancer-nat-rules"></a><span data-ttu-id="9e4a1-248">Tworzenie reguł NAT modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="9e4a1-248">Create load balancer NAT rules</span></span>
<span data-ttu-id="9e4a1-249">Aby uzyskać ruchu przepływających przez naszych modułu równoważenia obciążenia, należy utworzyć adres sieciowy reguł translacji adresów, które Określ akcje ruchu przychodzącego lub wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-249">To get traffic flowing through our load balancer, we need to create network address translation (NAT) rules that specify either inbound or outbound actions.</span></span> <span data-ttu-id="9e4a1-250">Należy określić protokół, który ma być używany, a następnie mapują porty zewnętrznych do wewnętrznych portów zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-250">You can specify the protocol to use, then map external ports to internal ports as desired.</span></span> <span data-ttu-id="9e4a1-251">W naszym środowisku Utwórzmy niektórych reguł, które umożliwiają SSH za pomocą naszej usługi równoważenia obciążenia do naszej maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-251">For our environment, let's create some rules that allow SSH through our load balancer to our VMs.</span></span> <span data-ttu-id="9e4a1-252">Skonfigurowanie portów TCP 4222 i 4223 do przekierowania do portu TCP 22 na naszych maszyn wirtualnych (które możemy utworzyć później).</span><span class="sxs-lookup"><span data-stu-id="9e4a1-252">We set up TCP ports 4222 and 4223 to direct to TCP port 22 on our VMs (which we create later).</span></span> <span data-ttu-id="9e4a1-253">Poniższy przykład tworzy reguły o nazwie `myLoadBalancerRuleSSH1` mapować TCP port 4222 port 22:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-253">The following example creates a rule named `myLoadBalancerRuleSSH1` to map TCP port 4222 to port 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

<span data-ttu-id="9e4a1-254">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-254">Output:</span></span>

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up the load balancer "myLoadBalancer"
warn:    Using default enable floating ip: false
warn:    Using default idle timeout: 4
warn:    Using default mySubnet IP configuration "myFrontEndPool"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleSSH1
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 4222
data:    Backend port                    : 22
data:    Enable floating IP              : false
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
info:    network lb inbound-nat-rule create command OK
```

<span data-ttu-id="9e4a1-255">Powtórz procedurę drugi reguły NAT dla SSH.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-255">Repeat the procedure for your second NAT rule for SSH.</span></span> <span data-ttu-id="9e4a1-256">Poniższy przykład tworzy reguły o nazwie `myLoadBalancerRuleSSH2` mapować TCP port 4223 port 22:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-256">The following example creates a rule named `myLoadBalancerRuleSSH2` to map TCP port 4223 to port 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

<span data-ttu-id="9e4a1-257">Umożliwia również Przejdź dalej i utworzyć regułę NAT dla portu TCP 80 dla ruchu w sieci web, przechwytywanie reguły do naszej pule adresów IP.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-257">Let's also go ahead and create a NAT rule for TCP port 80 for web traffic, hooking the rule up to our IP pools.</span></span> <span data-ttu-id="9e4a1-258">Jeśli firma Microsoft Podłączanie reguły pula IP, a Podłączanie reguły do naszej maszyn wirtualnych pojedynczo, firma Microsoft można dodawać i usuwać maszyn wirtualnych z puli adresów IP.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-258">If we hook up the rule to an IP pool, instead of hooking up the rule to our VMs individually, we can add or remove VMs from the IP pool.</span></span> <span data-ttu-id="9e4a1-259">Moduł równoważenia obciążenia jest automatycznie dostosowuje przepływu ruchu.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-259">The load balancer automatically adjusts the flow of traffic.</span></span> <span data-ttu-id="9e4a1-260">Poniższy przykład tworzy reguły o nazwie `myLoadBalancerRuleWeb` mapować TCP port 80 z portem 80:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-260">The following example creates a rule named `myLoadBalancerRuleWeb` to map TCP port 80 to port 80:</span></span>

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

<span data-ttu-id="9e4a1-261">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-261">Output:</span></span>

```azurecli
info:    Executing command network lb rule create
+ Looking up the load balancer "myLoadBalancer"
warn:    Using default idle timeout: 4
warn:    Using default enable floating ip: false
warn:    Using default load distribution: Default
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleWeb
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 80
data:    Backend port                    : 80
data:    Enable floating IP              : false
data:    Load distribution               : Default
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
data:    Backend address pool id         : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
info:    network lb rule create command OK
```

## <a name="create-a-load-balancer-health-probe"></a><span data-ttu-id="9e4a1-262">Utwórz kondycji sondę modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="9e4a1-262">Create a load balancer health probe</span></span>
<span data-ttu-id="9e4a1-263">Kondycję sondowania okresowo sprawdza na maszynach wirtualnych, które znajdują się za naszej usługi równoważenia obciążenia, aby upewnić się, ich działania i odpowiada na żądania, zgodnie z definicją.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-263">A health probe periodically checks on the VMs that are behind our load balancer to make sure they're operating and responding to requests as defined.</span></span> <span data-ttu-id="9e4a1-264">Jeśli nie, usuwane z operacji, aby upewnić się, że użytkownicy nie są być kierowany do nich.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-264">If not, they're removed from operation to ensure that users aren't being directed to them.</span></span> <span data-ttu-id="9e4a1-265">Można zdefiniować niestandardowe kontroli sondy kondycji, oraz odstępach czasu i wartości limitu czasu.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-265">You can define custom checks for the health probe, along with intervals and timeout values.</span></span> <span data-ttu-id="9e4a1-266">Aby uzyskać więcej informacji na temat sondy kondycji, zobacz [sondy modułu równoważenia obciążenia](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e4a1-266">For more information about health probes, see [Load Balancer probes](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="9e4a1-267">Poniższy przykład tworzy TCP kondycji sondowany o nazwie `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-267">The following example creates a TCP health probed named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

<span data-ttu-id="9e4a1-268">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-268">Output:</span></span>

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up the load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

<span data-ttu-id="9e4a1-269">W tym miejscu możemy określony interwał 15 sekund dla naszych kontroli kondycji.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-269">Here, we specified an interval of 15 seconds for our health checks.</span></span> <span data-ttu-id="9e4a1-270">Firma Microsoft może pominąć maksymalnie cztery sond (jedną minutę), zanim usługi równoważenia obciążenia uzna, że host nie działa.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-270">We can miss a maximum of four probes (one minute) before the load balancer considers that the host is no longer functioning.</span></span>

## <a name="verify-the-load-balancer"></a><span data-ttu-id="9e4a1-271">Sprawdź usługę równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="9e4a1-271">Verify the load balancer</span></span>
<span data-ttu-id="9e4a1-272">Po zakończeniu konfiguracji usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-272">Now the load balancer configuration is done.</span></span> <span data-ttu-id="9e4a1-273">Poniżej przedstawiono kroki wykonane:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-273">Here are the steps you took:</span></span>

1. <span data-ttu-id="9e4a1-274">Utworzono usługę równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-274">You created a load balancer.</span></span>
2. <span data-ttu-id="9e4a1-275">Utworzyć pulę IP frontonu i przypisane do publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-275">You created a front-end IP pool and assigned a public IP to it.</span></span>
3. <span data-ttu-id="9e4a1-276">Została utworzona pula adresów IP zaplecza, która maszyny wirtualne mogą nawiązać połączenie.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-276">You created a back-end IP pool that VMs can connect to.</span></span>
4. <span data-ttu-id="9e4a1-277">Utworzono reguł NAT, zezwalających na SSH z maszynami wirtualnymi zarządzania, oraz regułę zezwalającą port TCP 80 dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-277">You created NAT rules that allow SSH to the VMs for management, along with a rule that allows TCP port 80 for our web app.</span></span>
5. <span data-ttu-id="9e4a1-278">Po dodaniu sondy kondycji, aby okresowo sprawdzać maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-278">You added a health probe to periodically check the VMs.</span></span> <span data-ttu-id="9e4a1-279">To sondowanie kondycji gwarantuje, że użytkownicy nie próbują uzyskać dostęp maszynę Wirtualną, która jest już nie działa lub obsługę zawartości.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-279">This health probe ensures that users don't try to access a VM that is no longer functioning or serving content.</span></span>

<span data-ttu-id="9e4a1-280">Umożliwia przeglądanie jak teraz wygląda przez moduł równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-280">Let's review what your load balancer looks like now:</span></span>

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

<span data-ttu-id="9e4a1-281">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-281">Output:</span></span>

```json
{
  "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH1",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4222,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    },
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH2",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4223,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    }
  ],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "inboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        },
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleWeb",
      "provisioningState": "Succeeded",
      "enableFloatingIP": false,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "backendAddressPool": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
      },
      "protocol": "Tcp",
      "loadDistribution": "Default",
      "mySubnetPort": 80,
      "backendPort": 80,
      "idleTimeoutInMinutes": 4
    }
  ],
  "probes": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myHealthProbe",
      "provisioningState": "Succeeded",
      "numberOfProbes": 4,
      "intervalInSeconds": 15,
      "port": 80,
      "protocol": "Tcp",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/probes/myHealthProbe"
    }
  ]
}
```

## <a name="create-an-nic-to-use-with-the-linux-vm"></a><span data-ttu-id="9e4a1-282">Utwórz kartę Sieciową do użycia z maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="9e4a1-282">Create an NIC to use with the Linux VM</span></span>
<span data-ttu-id="9e4a1-283">Karty sieciowe są programowo dostępne, ponieważ reguły można stosować do ich używania.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-283">NICs are programmatically available because you can apply rules to their use.</span></span> <span data-ttu-id="9e4a1-284">Może także zawierać więcej niż jeden.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-284">You can also have more than one.</span></span> <span data-ttu-id="9e4a1-285">W następujących `azure network nic create` poleceń, podłącz kartę Sieciową do puli adresów IP zaplecza obciążenia i powiązać ją z reguły NAT, aby zezwolić na ruch protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-285">In the following `azure network nic create` command, you hook up the NIC to the load back-end IP pool and associate it with the NAT rule to permit SSH traffic.</span></span>

<span data-ttu-id="9e4a1-286">Zastąp `#####-###-###` sekcje z identyfikatorem subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9e4a1-286">Replace the `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="9e4a1-287">Identyfikator jest odnotowany w danych wyjściowych subskrypcji `jq` podczas badania tworzysz zasoby.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-287">Your subscription ID is noted in the output of `jq` when you examine the resources you are creating.</span></span> <span data-ttu-id="9e4a1-288">Można również wyświetlić identyfikator subskrypcji z `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-288">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="9e4a1-289">Poniższy przykład tworzy karty Sieciowej o nazwie `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-289">The following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

<span data-ttu-id="9e4a1-290">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-290">Output:</span></span>

```azurecli
info:    Executing command network nic create
+ Looking up the subnet "mySubnet"
+ Looking up the network interface "myNic1"
+ Creating network interface "myNic1"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1
data:    Name                            : myNic1
data:    Type                            : Microsoft.Network/networkInterfaces
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Enable IP forwarding            : false
data:    IP configurations:
data:      Name                          : Nic-IP-config
data:      Provisioning state            : Succeeded
data:      Private IP address            : 192.168.1.4
data:      Private IP allocation method  : Dynamic
data:      Subnet                        : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:      Load balancer backend address pools:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
data:      Load balancer inbound NAT rules:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
data:
info:    network nic create command OK
```

<span data-ttu-id="9e4a1-291">Można wyświetlić szczegóły, sprawdzając zasobu bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-291">You can see the details by examining the resource directly.</span></span> <span data-ttu-id="9e4a1-292">Zasób należy zbadać za pomocą `azure network nic show` polecenia:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-292">You examine the resource by using the `azure network nic show` command:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

<span data-ttu-id="9e4a1-293">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-293">Output:</span></span>

```json
{
  "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
  "provisioningState": "Succeeded",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1",
  "name": "myNic1",
  "type": "Microsoft.Network/networkInterfaces",
  "location": "westeurope",
  "ipConfigurations": [
    {
      "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1/ipConfigurations/Nic-IP-config",
      "loadBalancerBackendAddressPools": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
        }
      ],
      "loadBalancerInboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        }
      ],
      "privateIPAddress": "192.168.1.4",
      "privateIPAllocationMethod": "Dynamic",
      "subnet": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
      },
      "provisioningState": "Succeeded",
      "name": "Nic-IP-config"
    }
  ],
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": []
  },
  "enableIPForwarding": false,
  "resourceGuid": "a20258b8-6361-45f6-b1b4-27ffed28798c"
}
```

<span data-ttu-id="9e4a1-294">Teraz utworzymy drugiej karty Sieciowej, przechwytywanie w ponownie do naszej puli adresów IP zaplecza.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-294">Now we create the second NIC, hooking in to our back-end IP pool again.</span></span> <span data-ttu-id="9e4a1-295">Ta reguła NAT czasu druga zezwala na ruch protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-295">This time the second NAT rule permits SSH traffic.</span></span> <span data-ttu-id="9e4a1-296">Poniższy przykład tworzy karty Sieciowej o nazwie `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-296">The following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a><span data-ttu-id="9e4a1-297">Utwórz grupę zabezpieczeń sieci i reguł</span><span class="sxs-lookup"><span data-stu-id="9e4a1-297">Create a network security group and rules</span></span>
<span data-ttu-id="9e4a1-298">Teraz utworzymy sieciowej grupy zabezpieczeń i reguł ruchu przychodzącego, które kontrolują dostęp do karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-298">Now we create a network security group and the inbound rules that govern access to the NIC.</span></span> <span data-ttu-id="9e4a1-299">Grupa zabezpieczeń sieci może odnosić się do karty Sieciowej lub podsieci.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-299">A network security group can be applied to a NIC or subnet.</span></span> <span data-ttu-id="9e4a1-300">Należy zdefiniować regułę do sterowania przepływem ruch do i z maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-300">You define rules to control the flow of traffic in and out of your VMs.</span></span> <span data-ttu-id="9e4a1-301">Poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-301">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

<span data-ttu-id="9e4a1-302">Dodajmy regułę ruchu przychodzącego dla grupy NSG zezwolić na połączenia przychodzące do portu 22 (do obsługi protokołu SSH).</span><span class="sxs-lookup"><span data-stu-id="9e4a1-302">Let's add the inbound rule for the NSG to allow inbound connections on port 22 (to support SSH).</span></span> <span data-ttu-id="9e4a1-303">Poniższy przykład tworzy reguły o nazwie `myNetworkSecurityGroupRuleSSH` aby umożliwić ruch TCP na porcie 22:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-303">The following example creates a rule named `myNetworkSecurityGroupRuleSSH` to allow TCP on port 22:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

<span data-ttu-id="9e4a1-304">Teraz możemy dodać regułę ruchu przychodzącego dla grupy NSG zezwolić na połączenia przychodzące na porcie 80 (dla obsługi ruchu w sieci web).</span><span class="sxs-lookup"><span data-stu-id="9e4a1-304">Now let's add the inbound rule for the NSG to allow inbound connections on port 80 (to support web traffic).</span></span> <span data-ttu-id="9e4a1-305">Poniższy przykład tworzy reguły o nazwie `myNetworkSecurityGroupRuleHTTP` aby umożliwić ruch TCP na porcie 80:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-305">The following example creates a rule named `myNetworkSecurityGroupRuleHTTP` to allow TCP on port 80:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> <span data-ttu-id="9e4a1-306">Reguła ruchu przychodzącego jest filtrem dla połączeń sieciowych dla ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-306">The inbound rule is a filter for inbound network connections.</span></span> <span data-ttu-id="9e4a1-307">W tym przykładzie firma Microsoft powiązać grupa NSG maszyn wirtualnych wirtualnej karty Sieciowej, co oznacza, że każde żądanie port 22 jest przekazywana do karty interfejsu Sieciowego w przypadku naszego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-307">In this example, we bind the NSG to the VMs virtual NIC, which means that any request to port 22 is passed through to the NIC on our VM.</span></span> <span data-ttu-id="9e4a1-308">Tę regułę dla ruchu przychodzącego jest o połączenie sieciowe, a nie o punkt końcowy, który jest co byłoby o we wdrożeniach klasycznych.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-308">This inbound rule is about a network connection, and not about an endpoint, which is what it would be about in classic deployments.</span></span> <span data-ttu-id="9e4a1-309">Aby otworzyć port, należy pozostawić `--source-port-range` ustawioną "\*" (wartość domyślna) do akceptowania żądań przychodzących od **żadnych** żąda portu.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-309">To open a port, you must leave the `--source-port-range` set to '\*' (the default value) to accept inbound requests from **any** requesting port.</span></span> <span data-ttu-id="9e4a1-310">Porty są zwykle dynamiczne.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-310">Ports are typically dynamic.</span></span>
>
>

## <a name="bind-to-the-nic"></a><span data-ttu-id="9e4a1-311">Powiązanie z kartą sieciową</span><span class="sxs-lookup"><span data-stu-id="9e4a1-311">Bind to the NIC</span></span>
<span data-ttu-id="9e4a1-312">Grupa NSG należy powiązać karty interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-312">Bind the NSG to the NICs.</span></span> <span data-ttu-id="9e4a1-313">Należy połączyć z naszych kart sieciowych z naszej grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-313">We need to connect our NICs with our network security group.</span></span> <span data-ttu-id="9e4a1-314">Uruchom zarówno polecenia, aby Podłączanie obu naszych kart sieciowych:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-314">Run both commands, to hook up both of our NICs:</span></span>

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a><span data-ttu-id="9e4a1-315">Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="9e4a1-315">Create an availability set</span></span>
<span data-ttu-id="9e4a1-316">Zestawy dostępności rozpowszechniania pomocy maszyn wirtualnych w domenach awarii i domen uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-316">Availability sets help spread your VMs across fault domains and upgrade domains.</span></span> <span data-ttu-id="9e4a1-317">Utwórz zbiór dostępności dla maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-317">Let's create an availability set for your VMs.</span></span> <span data-ttu-id="9e4a1-318">Poniższy przykład tworzy zbiór nazwanego dostępności `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-318">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

<span data-ttu-id="9e4a1-319">Domen błędów Definiowanie grup maszyn wirtualnych, które współużytkują wspólne przełącznik źródła i sieci zasilania.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-319">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="9e4a1-320">Domyślnie maszyny wirtualne, które są skonfigurowane w zestawie dostępności są rozdzielone przez maksymalnie trzy domen błędów.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-320">By default, the virtual machines that are configured within your availability set are separated across up to three fault domains.</span></span> <span data-ttu-id="9e4a1-321">Ma to problemem sprzętowym w jednym z tych domen błędów nie wpływa na każdej maszynie Wirtualnej, która jest uruchomiona aplikacja.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-321">The idea is that a hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span> <span data-ttu-id="9e4a1-322">Azure automatycznie dystrybuuje maszyn wirtualnych w domenach awarii podczas umieszczania ich w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-322">Azure automatically distributes VMs across the fault domains when placing them in an availability set.</span></span>

<span data-ttu-id="9e4a1-323">Domen uaktualnienia wskazują grupy maszyn wirtualnych i podstawowym sprzętem fizycznym, który może zostać uruchomiony ponownie w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-323">Upgrade domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="9e4a1-324">Kolejność, w którym są ponownie uruchamiane domen uaktualnienia nie może być sekwencyjnych podczas zaplanowanej konserwacji, ale tylko jedno uaktualnienie ponownego uruchomienia w czasie.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-324">The order in which upgrade domains are rebooted might not be sequential during planned maintenance, but only one upgrade is rebooted at a time.</span></span> <span data-ttu-id="9e4a1-325">Ponownie Azure automatycznie dystrybuuje maszyn wirtualnych między domenami uaktualnienia podczas umieszczania ich w witrynie dostępności.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-325">Again, Azure automatically distributes your VMs across upgrade domains when placing them in an availability site.</span></span>

<span data-ttu-id="9e4a1-326">Przeczytaj więcej na temat [Zarządzanie dostępność maszyn wirtualnych](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e4a1-326">Read more about [managing the availability of VMs](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="create-the-linux-vms"></a><span data-ttu-id="9e4a1-327">Tworzenie maszyn wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="9e4a1-327">Create the Linux VMs</span></span>
<span data-ttu-id="9e4a1-328">Po utworzeniu magazynu i zasobów sieciowych do obsługi maszyn wirtualnych dostęp do Internetu.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-328">You've created the storage and network resources to support Internet-accessible VMs.</span></span> <span data-ttu-id="9e4a1-329">Teraz załóżmy tworzenie tych maszyn wirtualnych i zabezpieczenia przy użyciu klucza SSH, który nie ma hasła.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-329">Now let's create those VMs and secure them with an SSH key that doesn't have a password.</span></span> <span data-ttu-id="9e4a1-330">W takim przypadku zamierzamy utworzyć Ubuntu oparte na najnowszych LTS maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-330">In this case, we're going to create an Ubuntu VM based on the most recent LTS.</span></span> <span data-ttu-id="9e4a1-331">Możemy zlokalizować informacji obrazu przy użyciu `azure vm image list`, zgodnie z opisem w [znajdowanie obrazów maszyn wirtualnych Azure](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e4a1-331">We locate that image information by using `azure vm image list`, as described in [finding Azure VM images](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="9e4a1-332">Wybraliśmy obrazu za pomocą polecenia `azure vm image list westeurope canonical | grep LTS`.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-332">We selected an image by using the command `azure vm image list westeurope canonical | grep LTS`.</span></span> <span data-ttu-id="9e4a1-333">W takim przypadku stosujemy `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-333">In this case, we use `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span></span> <span data-ttu-id="9e4a1-334">W polu ostatniego jest przekazywana `latest` tak, aby w przyszłości zawsze uzyskujemy ostatniej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-334">For the last field, we pass `latest` so that in the future we always get the most recent build.</span></span> <span data-ttu-id="9e4a1-335">(Jest ciągiem używamy `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span><span class="sxs-lookup"><span data-stu-id="9e4a1-335">(The string we use is `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span></span>

<span data-ttu-id="9e4a1-336">Ten krok dalej jest znany dla każdego, kto został już utworzony ssh publicznego i prywatnego klucza rsa pary w systemie Linux lub Mac za pomocą **ssh-keygen - t rsa -b 2048**.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-336">This next step is familiar to anyone who has already created an ssh rsa public and private key pair on Linux or Mac by using **ssh-keygen -t rsa -b 2048**.</span></span> <span data-ttu-id="9e4a1-337">Jeśli nie masz żadnych certyfikatów pary kluczy Twojej `~/.ssh` katalogu, można je utworzyć:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-337">If you do not have any certificate key pairs in your `~/.ssh` directory, you can create them:</span></span>

* <span data-ttu-id="9e4a1-338">Automatycznie, przy użyciu `azure vm create --generate-ssh-keys` opcji.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-338">Automatically, by using the `azure vm create --generate-ssh-keys` option.</span></span>
* <span data-ttu-id="9e4a1-339">Ręcznie, używając [instrukcje, aby utworzyć samodzielnie](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e4a1-339">Manually, by using [the instructions to create them yourself](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="9e4a1-340">Alternatywnie można użyć `--admin-password` metody uwierzytelniania połączeń SSH, po utworzeniu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-340">Alternatively, you can use the `--admin-password` method to authenticate your SSH connections after the VM is created.</span></span> <span data-ttu-id="9e4a1-341">Ta metoda jest zazwyczaj mniej bezpieczna.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-341">This method is typically less secure.</span></span>

<span data-ttu-id="9e4a1-342">Utwórz maszynę Wirtualną przełączając naszych zasobów i informacji razem z `azure vm create` polecenia:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-342">We create the VM by bringing all our resources and information together with the `azure vm create` command:</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM1 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic1 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

<span data-ttu-id="9e4a1-343">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-343">Output:</span></span>

```azurecli
info:    Executing command vm create
+ Looking up the VM "myVM1"
info:    Verifying the public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using the VM Size "Standard_DS1"
info:    The [OS, Data] Disk or image configuration requires storage account
+ Looking up the storage account mystorageaccount
+ Looking up the availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up the NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in the NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    The storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by the parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

<span data-ttu-id="9e4a1-344">Podłączeniem do maszyny Wirtualnej bezpośrednio za pomocą kluczy SSH domyślne.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-344">You can connect to your VM immediately by using your default SSH keys.</span></span> <span data-ttu-id="9e4a1-345">Upewnij się, określ odpowiedni port, ponieważ firma Microsoft jest przekazanie za pośrednictwem usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-345">Make sure that you specify the appropriate port since we're passing through the load balancer.</span></span> <span data-ttu-id="9e4a1-346">(Dla naszych pierwsza maszyna wirtualna, możemy skonfigurować regułę NAT do przesyłania dalej portu 4222 do naszej maszyny Wirtualnej.)</span><span class="sxs-lookup"><span data-stu-id="9e4a1-346">(For our first VM, we set up the NAT rule to forward port 4222 to our VM.)</span></span>

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

<span data-ttu-id="9e4a1-347">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-347">Output:</span></span>

```bash
The authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

<span data-ttu-id="9e4a1-348">Przejdź dalej i utworzyć drugi maszyny Wirtualnej w taki sam sposób:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-348">Go ahead and create your second VM in the same manner:</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM2 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic2 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

<span data-ttu-id="9e4a1-349">I można teraz używać `azure vm show myResourceGroup myVM1` polecenie, aby sprawdzić, jakie zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-349">And you can now use the `azure vm show myResourceGroup myVM1` command to examine what you've created.</span></span> <span data-ttu-id="9e4a1-350">W tym momencie używasz Ubuntu maszyn wirtualnych za modułem równoważenia obciążenia w Azure, który użytkownik może zalogować się do tylko z Twojej pary kluczy SSH (ponieważ haseł są wyłączone).</span><span class="sxs-lookup"><span data-stu-id="9e4a1-350">At this point, you're running your Ubuntu VMs behind a load balancer in Azure that you can sign into only with your SSH key pair (because passwords are disabled).</span></span> <span data-ttu-id="9e4a1-351">Można zainstalować nginx lub host z wieloma adresami, wdrażanie aplikacji sieci web i widoczne ruchu przepływ przez moduł równoważenia obciążenia do obu maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-351">You can install nginx or httpd, deploy a web app, and see the traffic flow through the load balancer to both of the VMs.</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

<span data-ttu-id="9e4a1-352">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-352">Output:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up the VM "TestVM1"
+ Looking up the NIC "myNic1"
data:    Id                              :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Succeeded
data:    Name                            :myVM1
data:    Location                        :westeurope
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :16.04.0-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clib45a8b650f4428a1-os-1471973896525
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/clib45a8b650f4428a1-os-1471973896525.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-24-D4-AA
data:          Provisioning State        :Succeeded
data:          Name                      :LmyNic1
data:          Location                  :westeurope
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://mystorageaccount.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm show command OK

```


## <a name="export-the-environment-as-a-template"></a><span data-ttu-id="9e4a1-353">Eksportuj środowiska jako szablon</span><span class="sxs-lookup"><span data-stu-id="9e4a1-353">Export the environment as a template</span></span>
<span data-ttu-id="9e4a1-354">Teraz, dlatego utworzone to środowisko, co zrobić, jeśli chcesz utworzyć środowisko projektowe dodatkowych z takimi samymi parametrami lub środowiska produkcyjnego, odpowiadający jej?</span><span class="sxs-lookup"><span data-stu-id="9e4a1-354">Now that you have built out this environment, what if you want to create an additional development environment with the same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="9e4a1-355">Menedżer zasobów używa szablony JSON, które definiują wszystkie parametry dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-355">Resource Manager uses JSON templates that define all the parameters for your environment.</span></span> <span data-ttu-id="9e4a1-356">Limit całego środowiska kompilacji, umieszczając odwołanie do tego szablonu JSON.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-356">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="9e4a1-357">Możesz [ręcznie utworzyć szablony JSON](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub wyeksportować utworzenie szablonu JSON do istniejącego środowiska:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-357">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment to create the JSON template for you:</span></span>

```azurecli
azure group export --name myResourceGroup
```

<span data-ttu-id="9e4a1-358">To polecenie tworzy `myResourceGroup.json` plik w bieżącym katalogu roboczym.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-358">This command creates the `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="9e4a1-359">Podczas tworzenia środowiska z tego szablonu, wyświetlany jest monit dla wszystkich nazw zasobów, łącznie z nazwami dla usługi równoważenia obciążenia, interfejsów sieciowych lub maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-359">When you create an environment from this template, you are prompted for all the resource names, including the names for the load balancer, network interfaces, or VMs.</span></span> <span data-ttu-id="9e4a1-360">Można go wypełnić te nazwy w pliku szablonu, dodając `-p` lub `--includeParameterDefaultValue` parametr `azure group export` polecenia, która została przedstawiona wcześniej.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-360">You can populate these names in your template file by adding the `-p` or `--includeParameterDefaultValue` parameter to the `azure group export` command that was shown earlier.</span></span> <span data-ttu-id="9e4a1-361">Edytuj szablon JSON można określić nazwy zasobu lub [Tworzenie pliku parameters.JSON następującym kodem](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) , który określa nazwy zasobu.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-361">Edit your JSON template to specify the resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies the resource names.</span></span>

<span data-ttu-id="9e4a1-362">Aby utworzyć środowisko z szablonu:</span><span class="sxs-lookup"><span data-stu-id="9e4a1-362">To create an environment from your template:</span></span>

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

<span data-ttu-id="9e4a1-363">Warto przeczytać [więcej informacji na temat sposobu wdrażania z szablonów](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e4a1-363">You might want to read [more about how to deploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="9e4a1-364">Więcej informacji na temat sposobu przyrostowo aktualizacja środowisk, użyj pliku parametrów i dostępu do szablonów z lokalizacji magazynu jednego.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-364">Learn about how to incrementally update environments, use the parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e4a1-365">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9e4a1-365">Next steps</span></span>
<span data-ttu-id="9e4a1-366">Teraz możesz przystąpić do rozpoczęcia pracy z wieloma składnikami sieciowymi i maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-366">Now you're ready to begin working with multiple networking components and VMs.</span></span> <span data-ttu-id="9e4a1-367">To środowisko próbki służy do tworzenia aplikacji przy użyciu podstawowe składniki wprowadzone w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="9e4a1-367">You can use this sample environment to build out your application by using the core components introduced here.</span></span>
