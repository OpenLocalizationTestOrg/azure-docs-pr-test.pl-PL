---
title: "aaaCreate kompletne środowisko Linux z hello Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Tworzenie magazynu, Maszynę wirtualną systemu Linux, sieci wirtualnej i podsieci, usługi równoważenia obciążenia, karty Sieciowej, publicznego adresu IP i sieciową grupę zabezpieczeń, z hello tła przy użyciu hello Azure CLI w wersji 1.0."
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
ms.openlocfilehash: 7fe00e138704fe9c9a1c9b87a7dd1afd6174e527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-environment-with-hello-azure-cli-10"></a><span data-ttu-id="0e471-103">Utwórz pełną środowiska Linux z hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="0e471-103">Create a complete Linux environment with hello Azure CLI 1.0</span></span>
<span data-ttu-id="0e471-104">W tym artykule budujemy prosta sieć z modułem równoważenia obciążenia i para maszyn wirtualnych, które są przydatne w przypadku tworzenia i przetwarzania proste.</span><span class="sxs-lookup"><span data-stu-id="0e471-104">In this article, we build a simple network with a load balancer and a pair of VMs that are useful for development and simple computing.</span></span> <span data-ttu-id="0e471-105">Firma Microsoft przeprowadzenie procesu hello przez polecenie, dopóki nie uzyskasz dwóch pracy zabezpieczeń toowhich maszyn wirtualnych systemu Linux, które można połączyć z dowolnego miejsca w hello Internet.</span><span class="sxs-lookup"><span data-stu-id="0e471-105">We walk through hello process command by command, until you have two working, secure Linux VMs toowhich you can connect from anywhere on hello Internet.</span></span> <span data-ttu-id="0e471-106">Następnie można przenieść na toomore złożone sieci i środowiskach.</span><span class="sxs-lookup"><span data-stu-id="0e471-106">Then you can move on toomore complex networks and environments.</span></span>

<span data-ttu-id="0e471-107">Wzdłuż sposób hello zapoznanie się hello zależności hierarchii modelu wdrażania usługi Resource Manager hello umożliwia, czy o ile zawiera.</span><span class="sxs-lookup"><span data-stu-id="0e471-107">Along hello way, you learn about hello dependency hierarchy that hello Resource Manager deployment model gives you, and about how much power it provides.</span></span> <span data-ttu-id="0e471-108">Po jak hello system jest wbudowana, można go znacznie szybciej odtworzyć za pomocą [szablonów usługi Azure Resource Manager](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0e471-108">After you see how hello system is built, you can rebuild it much more quickly by using [Azure Resource Manager templates](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="0e471-109">Ponadto po dowiesz się, jak hello części środowiska dopasowania, tworzenie szablonów tooautomate ich staje się łatwiejsze.</span><span class="sxs-lookup"><span data-stu-id="0e471-109">Also, after you learn how hello parts of your environment fit together, creating templates tooautomate them becomes easier.</span></span>

<span data-ttu-id="0e471-110">środowisko Hello zawiera:</span><span class="sxs-lookup"><span data-stu-id="0e471-110">hello environment contains:</span></span>

* <span data-ttu-id="0e471-111">Dwie maszyny wirtualne w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="0e471-111">Two VMs inside an availability set.</span></span>
* <span data-ttu-id="0e471-112">Usługi równoważenia obciążenia z regułą równoważenia obciążenia na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="0e471-112">A load balancer with a load-balancing rule on port 80.</span></span>
* <span data-ttu-id="0e471-113">Grupy zabezpieczeń sieci (NSG) zasady tooprotect maszyny Wirtualnej z niepożądanego ruchu.</span><span class="sxs-lookup"><span data-stu-id="0e471-113">Network security group (NSG) rules tooprotect your VM from unwanted traffic.</span></span>

<span data-ttu-id="0e471-114">toocreate to środowisko niestandardowe, należy hello najnowszych [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) w trybie Menedżera zasobów (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="0e471-114">toocreate this custom environment, you need hello latest [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in Resource Manager mode (`azure config mode arm`).</span></span> <span data-ttu-id="0e471-115">Należy również JSON, narzędzie do analizy.</span><span class="sxs-lookup"><span data-stu-id="0e471-115">You also need a JSON parsing tool.</span></span> <span data-ttu-id="0e471-116">W tym przykładzie użyto [jq](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="0e471-116">This example uses [jq](https://stedolan.github.io/jq/).</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="0e471-117">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="0e471-117">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="0e471-118">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="0e471-118">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="0e471-119">[Azure CLI 1.0](#quick-commands) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="0e471-119">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="0e471-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="0e471-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="0e471-121">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="0e471-121">Quick commands</span></span>
<span data-ttu-id="0e471-122">Jeśli potrzebujesz tooquickly hello zadania, powitania po sekcji Szczegóły hello podstawowych poleceń tooupload tooAzure maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0e471-122">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VM tooAzure.</span></span> <span data-ttu-id="0e471-123">Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć w rest hello hello dokumentu, początkowa [tutaj](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="0e471-123">More detailed information and context for each step can be found in hello rest of hello document, starting [here](#detailed-walkthrough).</span></span>

<span data-ttu-id="0e471-124">Upewnij się, że masz [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) zalogowany i w trybie Menedżera zasobów:</span><span class="sxs-lookup"><span data-stu-id="0e471-124">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="0e471-125">Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="0e471-125">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="0e471-126">Przykład nazwy parametru zawierają `myResourceGroup`, `mystorageaccount`, i `myVM`.</span><span class="sxs-lookup"><span data-stu-id="0e471-126">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

<span data-ttu-id="0e471-127">Utwórz grupę zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="0e471-127">Create hello resource group.</span></span> <span data-ttu-id="0e471-128">Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `westeurope` lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="0e471-128">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location:</span></span>

```azurecli
azure group create -n myResourceGroup -l westeurope
```

<span data-ttu-id="0e471-129">Sprawdź hello grupy zasobów, przy użyciu analizatora składni JSON hello:</span><span class="sxs-lookup"><span data-stu-id="0e471-129">Verify hello resource group by using hello JSON parser:</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="0e471-130">Tworzenie konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="0e471-130">Create hello storage account.</span></span> <span data-ttu-id="0e471-131">Witaj poniższy przykład tworzy konto magazynu o nazwie `mystorageaccount`.</span><span class="sxs-lookup"><span data-stu-id="0e471-131">hello following example creates a storage account named `mystorageaccount`.</span></span> <span data-ttu-id="0e471-132">(nazwa konta magazynu hello musi być unikatowa, aby podać własną unikatową nazwę.)</span><span class="sxs-lookup"><span data-stu-id="0e471-132">(hello storage account name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

<span data-ttu-id="0e471-133">Sprawdź konto magazynu hello przy użyciu analizatora składni JSON hello:</span><span class="sxs-lookup"><span data-stu-id="0e471-133">Verify hello storage account by using hello JSON parser:</span></span>

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

<span data-ttu-id="0e471-134">Utwórz sieć wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="0e471-134">Create hello virtual network.</span></span> <span data-ttu-id="0e471-135">Witaj poniższy przykład tworzy sieć wirtualną o nazwie `myVnet`:</span><span class="sxs-lookup"><span data-stu-id="0e471-135">hello following example creates a virtual network named `myVnet`:</span></span>

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

<span data-ttu-id="0e471-136">Utwórz podsieć.</span><span class="sxs-lookup"><span data-stu-id="0e471-136">Create a subnet.</span></span> <span data-ttu-id="0e471-137">Witaj poniższy przykład tworzy podsieć o nazwie `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="0e471-137">hello following example creates a subnet named `mySubnet`:</span></span>

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

<span data-ttu-id="0e471-138">Sprawdź hello sieci wirtualnej i podsieci przy użyciu analizatora składni JSON hello:</span><span class="sxs-lookup"><span data-stu-id="0e471-138">Verify hello virtual network and subnet by using hello JSON parser:</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="0e471-139">Tworzenie publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="0e471-139">Create a public IP.</span></span> <span data-ttu-id="0e471-140">Witaj poniższy przykład tworzy publicznego adresu IP o nazwie `myPublicIP` o nazwie DNS hello `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="0e471-140">hello following example creates a public IP named `myPublicIP` with hello DNS name of `mypublicdns`.</span></span> <span data-ttu-id="0e471-141">(nazwa DNS hello musi być unikatowa, aby podać własną unikatową nazwę.)</span><span class="sxs-lookup"><span data-stu-id="0e471-141">(hello DNS name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

<span data-ttu-id="0e471-142">Utwórz hello modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="0e471-142">Create hello load balancer.</span></span> <span data-ttu-id="0e471-143">Witaj poniższy przykład tworzy moduł równoważenia obciążenia o nazwie `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="0e471-143">hello following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

<span data-ttu-id="0e471-144">Utwórz pulę IP frontonu dla usługi równoważenia obciążenia hello i skojarz hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="0e471-144">Create a front-end IP pool for hello load balancer, and associate hello public IP.</span></span> <span data-ttu-id="0e471-145">Witaj poniższy przykład tworzy frontonu pula IP o nazwie `mySubnetPool`:</span><span class="sxs-lookup"><span data-stu-id="0e471-145">hello following example creates a front-end IP pool named `mySubnetPool`:</span></span>

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

<span data-ttu-id="0e471-146">Tworzenie puli adresów IP zaplecza powitania dla usługi równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="0e471-146">Create hello back-end IP pool for hello load balancer.</span></span> <span data-ttu-id="0e471-147">Witaj poniższy przykład tworzy pula IP zaplecza, o nazwie `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="0e471-147">hello following example creates a back-end IP pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

<span data-ttu-id="0e471-148">Tworzenie sieci dla ruchu przychodzącego protokołu SSH reguł translacji adresów adres hello modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="0e471-148">Create SSH inbound network address translation (NAT) rules for hello load balancer.</span></span> <span data-ttu-id="0e471-149">Witaj poniższy przykład tworzy dwie reguły modułu równoważenia obciążenia, `myLoadBalancerRuleSSH1` i `myLoadBalancerRuleSSH2`:</span><span class="sxs-lookup"><span data-stu-id="0e471-149">hello following example creates two load balancer rules, `myLoadBalancerRuleSSH1` and `myLoadBalancerRuleSSH2`:</span></span>

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

<span data-ttu-id="0e471-150">Tworzenie sieci web hello reguły NAT ruchu przychodzącego dla hello modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="0e471-150">Create hello web inbound NAT rules for hello load balancer.</span></span> <span data-ttu-id="0e471-151">Witaj poniższy przykład tworzy regułę równoważenia obciążenia o nazwie `myLoadBalancerRuleWeb`:</span><span class="sxs-lookup"><span data-stu-id="0e471-151">hello following example creates a load balancer rule named `myLoadBalancerRuleWeb`:</span></span>

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

<span data-ttu-id="0e471-152">Utwórz sondy kondycji modułu równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="0e471-152">Create hello load balancer health probe.</span></span> <span data-ttu-id="0e471-153">Witaj poniższy przykład tworzy sondowaniem TCP o nazwie `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="0e471-153">hello following example creates a TCP probe named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

<span data-ttu-id="0e471-154">Sprawdź hello modułu równoważenia obciążenia, pule adresów IP i reguł NAT, za pomocą analizatora składni JSON hello:</span><span class="sxs-lookup"><span data-stu-id="0e471-154">Verify hello load balancer, IP pools, and NAT rules by using hello JSON parser:</span></span>

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

<span data-ttu-id="0e471-155">Utwórz hello pierwszy karta sieciowa (NIC).</span><span class="sxs-lookup"><span data-stu-id="0e471-155">Create hello first network interface card (NIC).</span></span> <span data-ttu-id="0e471-156">Zastąp hello `#####-###-###` sekcje z identyfikatorem subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0e471-156">Replace hello `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="0e471-157">Identyfikator jest odnotowany w danych wyjściowych hello subskrypcji **jq** podczas badania zasobów hello tworzenia.</span><span class="sxs-lookup"><span data-stu-id="0e471-157">Your subscription ID is noted in hello output of **jq** when you examine hello resources you are creating.</span></span> <span data-ttu-id="0e471-158">Można również wyświetlić identyfikator subskrypcji z `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="0e471-158">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="0e471-159">Witaj poniższy przykład tworzy karty Sieciowej o nazwie `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="0e471-159">hello following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

<span data-ttu-id="0e471-160">Utwórz hello drugiej karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="0e471-160">Create hello second NIC.</span></span> <span data-ttu-id="0e471-161">Witaj poniższy przykład tworzy karty Sieciowej o nazwie `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="0e471-161">hello following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

<span data-ttu-id="0e471-162">Sprawdź Witaj dwie karty sieciowe za pomocą analizatora składni JSON hello:</span><span class="sxs-lookup"><span data-stu-id="0e471-162">Verify hello two NICs by using hello JSON parser:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

<span data-ttu-id="0e471-163">Utwórz grupę zabezpieczeń sieci hello.</span><span class="sxs-lookup"><span data-stu-id="0e471-163">Create hello network security group.</span></span> <span data-ttu-id="0e471-164">Witaj poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="0e471-164">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

<span data-ttu-id="0e471-165">Dodaj dwie reguły ruchu przychodzącego hello sieciowej grupy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="0e471-165">Add two inbound rules for hello network security group.</span></span> <span data-ttu-id="0e471-166">Witaj poniższy przykład tworzy dwie reguły `myNetworkSecurityGroupRuleSSH` i `myNetworkSecurityGroupRuleHTTP`:</span><span class="sxs-lookup"><span data-stu-id="0e471-166">hello following example creates two rules, `myNetworkSecurityGroupRuleSSH` and `myNetworkSecurityGroupRuleHTTP`:</span></span>

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

<span data-ttu-id="0e471-167">Sprawdź hello sieciowej grupy zabezpieczeń i reguł ruchu przychodzącego przy użyciu analizatora składni JSON hello:</span><span class="sxs-lookup"><span data-stu-id="0e471-167">Verify hello network security group and inbound rules by using hello JSON parser:</span></span>

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

<span data-ttu-id="0e471-168">Powiązania zabezpieczeń sieciowych hello grupy toohello dwie karty sieciowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-168">Bind hello network security group toohello two NICs:</span></span>

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

<span data-ttu-id="0e471-169">Utwórz hello zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="0e471-169">Create hello availability set.</span></span> <span data-ttu-id="0e471-170">Witaj poniższy przykład tworzy zbiór nazwanego dostępności `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="0e471-170">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

<span data-ttu-id="0e471-171">Tworzenie pierwszej maszyny Wirtualnej systemu Linux hello.</span><span class="sxs-lookup"><span data-stu-id="0e471-171">Create hello first Linux VM.</span></span> <span data-ttu-id="0e471-172">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM1`:</span><span class="sxs-lookup"><span data-stu-id="0e471-172">hello following example creates a VM named `myVM1`:</span></span>

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

<span data-ttu-id="0e471-173">Utwórz hello drugie maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="0e471-173">Create hello second Linux VM.</span></span> <span data-ttu-id="0e471-174">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM2`:</span><span class="sxs-lookup"><span data-stu-id="0e471-174">hello following example creates a VM named `myVM2`:</span></span>

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

<span data-ttu-id="0e471-175">Użyj tooverify analizatora składni JSON hello, że wszystko, który został utworzony:</span><span class="sxs-lookup"><span data-stu-id="0e471-175">Use hello JSON parser tooverify that everything that was built:</span></span>

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

<span data-ttu-id="0e471-176">Eksportowanie z nowego środowiska tooa szablonu tooquickly ponownie utworzyć nowych wystąpień:</span><span class="sxs-lookup"><span data-stu-id="0e471-176">Export your new environment tooa template tooquickly re-create new instances:</span></span>

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="0e471-177">Szczegółowy przewodnik</span><span class="sxs-lookup"><span data-stu-id="0e471-177">Detailed walkthrough</span></span>
<span data-ttu-id="0e471-178">Witaj szczegółowy opis kroków, które należy wykonać wyjaśnić, każdego polecenia czynności podczas tworzenia Twoje środowisko.</span><span class="sxs-lookup"><span data-stu-id="0e471-178">hello detailed steps that follow explain what each command is doing as you build out your environment.</span></span> <span data-ttu-id="0e471-179">Te pojęcia są przydatne podczas tworzenia własnego niestandardowego środowiska dla rozwoju lub produkcji.</span><span class="sxs-lookup"><span data-stu-id="0e471-179">These concepts are helpful when you build your own custom environments for development or production.</span></span>

<span data-ttu-id="0e471-180">Upewnij się, że masz [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) zalogowany i w trybie Menedżera zasobów:</span><span class="sxs-lookup"><span data-stu-id="0e471-180">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="0e471-181">Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="0e471-181">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="0e471-182">Przykład nazwy parametru zawierają `myResourceGroup`, `mystorageaccount`, i `myVM`.</span><span class="sxs-lookup"><span data-stu-id="0e471-182">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

## <a name="create-resource-groups-and-choose-deployment-locations"></a><span data-ttu-id="0e471-183">Tworzenie grupy zasobów, a następnie wybierz pozycję lokalizacji wdrożenia</span><span class="sxs-lookup"><span data-stu-id="0e471-183">Create resource groups and choose deployment locations</span></span>
<span data-ttu-id="0e471-184">Grupy zasobów platformy Azure są jednostki logicznej wdrożenia, które zawiera informacje i metadanych tooenable hello logiczny zarządzania konfiguracją wdrożeń zasobów.</span><span class="sxs-lookup"><span data-stu-id="0e471-184">Azure resource groups are logical deployment entities that contain configuration information and metadata tooenable hello logical management of resource deployments.</span></span> <span data-ttu-id="0e471-185">Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `westeurope` lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="0e471-185">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location:</span></span>

```azurecli
azure group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="0e471-186">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-186">Output:</span></span>

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

## <a name="create-a-storage-account"></a><span data-ttu-id="0e471-187">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="0e471-187">Create a storage account</span></span>
<span data-ttu-id="0e471-188">Potrzebujesz konta usługi storage dla dysków maszyny Wirtualnej i dla dowolnego dodatkowego dysku z danymi, które mają tooadd.</span><span class="sxs-lookup"><span data-stu-id="0e471-188">You need storage accounts for your VM disks and for any additional data disks that you want tooadd.</span></span> <span data-ttu-id="0e471-189">Możesz utworzyć konta magazynu prawie natychmiast po utworzeniu grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="0e471-189">You create storage accounts almost immediately after you create resource groups.</span></span>

<span data-ttu-id="0e471-190">W tym miejscu użyjemy hello `azure storage account create` polecenia przekazywanie hello Lokalizacja konta hello, hello grupy zasobów, która kontroluje, a typ hello obsługi magazynu ma.</span><span class="sxs-lookup"><span data-stu-id="0e471-190">Here we use hello `azure storage account create` command, passing hello location of hello account, hello resource group that controls it, and hello type of storage support you want.</span></span> <span data-ttu-id="0e471-191">Witaj poniższy przykład tworzy konto magazynu o nazwie `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="0e471-191">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

<span data-ttu-id="0e471-192">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-192">Output:</span></span>

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

<span data-ttu-id="0e471-193">tooexamine zasobów naszej grupy za pomocą hello `azure group show` polecenia, można użyć hello [jq](https://stedolan.github.io/jq/) narzędzia wraz z hello `--json` opcji wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0e471-193">tooexamine our resource group by using hello `azure group show` command, let's use hello [jq](https://stedolan.github.io/jq/) tool along with hello `--json` Azure CLI option.</span></span> <span data-ttu-id="0e471-194">(Można użyć **jsawk** lub żadnej biblioteki języka wolisz tooparse hello JSON.)</span><span class="sxs-lookup"><span data-stu-id="0e471-194">(You can use **jsawk** or any language library you prefer tooparse hello JSON.)</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="0e471-195">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-195">Output:</span></span>

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

<span data-ttu-id="0e471-196">tooinvestigate hello konta magazynu przy użyciu interfejsu wiersza polecenia hello, musisz najpierw nazwy kont hello tooset i kluczy.</span><span class="sxs-lookup"><span data-stu-id="0e471-196">tooinvestigate hello storage account by using hello CLI, you first need tooset hello account names and keys.</span></span> <span data-ttu-id="0e471-197">Zastąp hello nazwy konta magazynu hello w hello poniższy przykład o nazwie, wybrane:</span><span class="sxs-lookup"><span data-stu-id="0e471-197">Replace hello name of hello storage account in hello following example with a name that you choose:</span></span>

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

<span data-ttu-id="0e471-198">Następnie można wyświetlić informacje o pamięci masowej łatwo:</span><span class="sxs-lookup"><span data-stu-id="0e471-198">Then you can view your storage information easily:</span></span>

```azurecli
azure storage container list
```

<span data-ttu-id="0e471-199">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-199">Output:</span></span>

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="0e471-200">Tworzenie sieci wirtualnej i podsieci</span><span class="sxs-lookup"><span data-stu-id="0e471-200">Create a virtual network and subnet</span></span>
<span data-ttu-id="0e471-201">Następnie będzie tooneed toocreate sieci wirtualnej z systemem Azure i podsieć, w którym można utworzyć maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="0e471-201">Next you're going tooneed toocreate a virtual network running in Azure and a subnet in which you can create your VMs.</span></span> <span data-ttu-id="0e471-202">Witaj poniższy przykład tworzy sieć wirtualną o nazwie `myVnet` z hello `192.168.0.0/16` prefiks adresu:</span><span class="sxs-lookup"><span data-stu-id="0e471-202">hello following example creates a virtual network named `myVnet` with hello `192.168.0.0/16` address prefix:</span></span>

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="0e471-203">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-203">Output:</span></span>

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

<span data-ttu-id="0e471-204">Użyjmy ponownie, opcja--json hello `azure group show` i `jq` toosee jak tworzymy naszych zasobów.</span><span class="sxs-lookup"><span data-stu-id="0e471-204">Again, let's use hello --json option of `azure group show` and `jq` toosee how we're building our resources.</span></span> <span data-ttu-id="0e471-205">Teraz `storageAccounts` zasobów i `virtualNetworks` zasobów.</span><span class="sxs-lookup"><span data-stu-id="0e471-205">We now have a `storageAccounts` resource and a `virtualNetworks` resource.</span></span>  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="0e471-206">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-206">Output:</span></span>

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

<span data-ttu-id="0e471-207">Teraz Utwórzmy podsieci w hello `myVnet` sieci wirtualnej, w których hello wdrożonych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="0e471-207">Now let's create a subnet in hello `myVnet` virtual network into which hello VMs are deployed.</span></span> <span data-ttu-id="0e471-208">Używamy hello `azure network vnet subnet create` polecenia wraz z zasobów hello już utworzyliśmy: hello `myResourceGroup` grupy zasobów i hello `myVnet` sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0e471-208">We use hello `azure network vnet subnet create` command, along with hello resources we've already created: hello `myResourceGroup` resource group and hello `myVnet` virtual network.</span></span> <span data-ttu-id="0e471-209">W hello poniższy przykład, możemy dodać hello podsieci o nazwie `mySubnet` z prefiksu adresu podsieci hello `192.168.1.0/24`:</span><span class="sxs-lookup"><span data-stu-id="0e471-209">In hello following example, we add hello subnet named `mySubnet` with hello subnet address prefix of `192.168.1.0/24`:</span></span>

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

<span data-ttu-id="0e471-210">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-210">Output:</span></span>

```azurecli
info:    Executing command network vnet subnet create
+ Looking up hello subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up hello subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

<span data-ttu-id="0e471-211">Ponieważ podsieci hello logicznie znajduje się w sieci wirtualnej hello, możemy znaleźć hello podsieci za pomocą polecenia nieco inne.</span><span class="sxs-lookup"><span data-stu-id="0e471-211">Because hello subnet is logically inside hello virtual network, we look for hello subnet information with a slightly different command.</span></span> <span data-ttu-id="0e471-212">polecenie Hello używamy jest `azure network vnet show`, ale nadal dane wyjściowe JSON hello tooexamine przy użyciu `jq`.</span><span class="sxs-lookup"><span data-stu-id="0e471-212">hello command we use is `azure network vnet show`, but we continue tooexamine hello JSON output by using `jq`.</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="0e471-213">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-213">Output:</span></span>

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

## <a name="create-a-public-ip-address"></a><span data-ttu-id="0e471-214">Tworzenie publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="0e471-214">Create a public IP address</span></span>
<span data-ttu-id="0e471-215">Teraz Utwórzmy hello publicznego adresu IP (PIP) czy możemy przypisać tooyour modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="0e471-215">Now let's create hello public IP address (PIP) that we assign tooyour load balancer.</span></span> <span data-ttu-id="0e471-216">Włącza tooconnect tooyour maszyn wirtualnych z hello Internet przy użyciu hello `azure network public-ip create` polecenia.</span><span class="sxs-lookup"><span data-stu-id="0e471-216">It enables you tooconnect tooyour VMs from hello Internet by using hello `azure network public-ip create` command.</span></span> <span data-ttu-id="0e471-217">Ponieważ hello domyślnym adresem jest dynamiczny, utworzymy nazwany wpis DNS w hello **cloudapp.azure.com** domeny przy użyciu hello `--domain-name-label` opcji.</span><span class="sxs-lookup"><span data-stu-id="0e471-217">Because hello default address is dynamic, we create a named DNS entry in hello **cloudapp.azure.com** domain by using hello `--domain-name-label` option.</span></span> <span data-ttu-id="0e471-218">Witaj poniższy przykład tworzy publicznego adresu IP o nazwie `myPublicIP` o nazwie DNS hello `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="0e471-218">hello following example creates a public IP named `myPublicIP` with hello DNS name of `mypublicdns`.</span></span> <span data-ttu-id="0e471-219">Nazwa DNS hello musi być unikatowa, należy dostarczyć własną unikatową nazwę DNS:</span><span class="sxs-lookup"><span data-stu-id="0e471-219">Because hello DNS name must be unique, you provide your own unique DNS name:</span></span>

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

<span data-ttu-id="0e471-220">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-220">Output:</span></span>

```azurecli
info:    Executing command network public-ip create
+ Looking up hello public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up hello public ip "myPublicIP"
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

<span data-ttu-id="0e471-221">Hello publiczny adres IP jest również zasobem najwyższego poziomu, tak aby było widać, z `azure group show`.</span><span class="sxs-lookup"><span data-stu-id="0e471-221">hello public IP address is also a top-level resource, so you can see it with `azure group show`.</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="0e471-222">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-222">Output:</span></span>

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

<span data-ttu-id="0e471-223">Więcej szczegółów zasobów, w tym hello pełną nazwę domeny (FQDN) domeny podrzędnej hello, za pomocą hello pełną można zbadać `azure network public-ip show` polecenia.</span><span class="sxs-lookup"><span data-stu-id="0e471-223">You can investigate more resource details, including hello fully qualified domain name (FQDN) of hello subdomain, by using hello complete `azure network public-ip show` command.</span></span> <span data-ttu-id="0e471-224">została przydzielona logicznie Hello zasobu publicznego adresu IP, ale nie został jeszcze przypisany określony adres.</span><span class="sxs-lookup"><span data-stu-id="0e471-224">hello public IP address resource has been allocated logically, but a specific address has not yet been assigned.</span></span> <span data-ttu-id="0e471-225">tooobtain adresu IP, który ma tooneed modułu równoważenia obciążenia, które firma Microsoft nie został jeszcze utworzony.</span><span class="sxs-lookup"><span data-stu-id="0e471-225">tooobtain an IP address, you're going tooneed a load balancer, which we have not yet created.</span></span>

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

<span data-ttu-id="0e471-226">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-226">Output:</span></span>

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

## <a name="create-a-load-balancer-and-ip-pools"></a><span data-ttu-id="0e471-227">Tworzenie modułu równoważenia obciążenia i pule adresów IP</span><span class="sxs-lookup"><span data-stu-id="0e471-227">Create a load balancer and IP pools</span></span>
<span data-ttu-id="0e471-228">Podczas tworzenia modułu równoważenia obciążenia, umożliwia toodistribute ruchu między wieloma maszynami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="0e471-228">When you create a load balancer, it enables you toodistribute traffic across multiple VMs.</span></span> <span data-ttu-id="0e471-229">Udostępnia również nadmiarowość tooyour aplikacji, uruchamiając wiele maszyn wirtualnych, które odpowiadać toouser żądań w zdarzeniu hello konserwacji lub dużym obciążeniem.</span><span class="sxs-lookup"><span data-stu-id="0e471-229">It also provides redundancy tooyour application by running multiple VMs that respond toouser requests in hello event of maintenance or heavy loads.</span></span> <span data-ttu-id="0e471-230">Witaj poniższy przykład tworzy moduł równoważenia obciążenia o nazwie `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="0e471-230">hello following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

<span data-ttu-id="0e471-231">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-231">Output:</span></span>

```azurecli
info:    Executing command network lb create
+ Looking up hello load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

<span data-ttu-id="0e471-232">Naszej usługi równoważenia obciążenia jest dość pusty, więc warto utworzyć niektóre pule adresów IP.</span><span class="sxs-lookup"><span data-stu-id="0e471-232">Our load balancer is fairly empty, so let's create some IP pools.</span></span> <span data-ttu-id="0e471-233">Chcemy toocreate dwa pule adresów IP dla naszej usługi równoważenia obciążenia, jedno dla hello frontonu i jeden dla hello zaplecza.</span><span class="sxs-lookup"><span data-stu-id="0e471-233">We want toocreate two IP pools for our load balancer, one for hello front end and one for hello back end.</span></span> <span data-ttu-id="0e471-234">puli adresów IP frontonu Hello jest publicznie widoczna.</span><span class="sxs-lookup"><span data-stu-id="0e471-234">hello front-end IP pool is publicly visible.</span></span> <span data-ttu-id="0e471-235">Możliwe jest również hello toowhich lokalizacji, które możemy przypisać hello PIP utworzonej wcześniej.</span><span class="sxs-lookup"><span data-stu-id="0e471-235">It's also hello location toowhich we assign hello PIP that we created earlier.</span></span> <span data-ttu-id="0e471-236">Następnie używamy puli zaplecza hello jako lokalizacji dla naszej tooconnect maszyn wirtualnych do.</span><span class="sxs-lookup"><span data-stu-id="0e471-236">Then we use hello back-end pool as a location for our VMs tooconnect to.</span></span> <span data-ttu-id="0e471-237">W ten sposób hello ruch mógł przepływać przez toohello usługi równoważenia obciążenia hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="0e471-237">That way, hello traffic can flow through hello load balancer toohello VMs.</span></span>

<span data-ttu-id="0e471-238">Najpierw utwórz naszych frontonu puli adresów IP.</span><span class="sxs-lookup"><span data-stu-id="0e471-238">First, let's create our front-end IP pool.</span></span> <span data-ttu-id="0e471-239">Witaj poniższy przykład tworzy puli frontonu o nazwie `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="0e471-239">hello following example creates a front-end pool named `myFrontEndPool`:</span></span>

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

<span data-ttu-id="0e471-240">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-240">Output:</span></span>

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up hello load balancer "myLoadBalancer"
+ Looking up hello public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

<span data-ttu-id="0e471-241">Należy zwrócić uwagę, jak użyliśmy hello `--public-ip-name` przełącznika toopass w hello `myPublicIP` utworzonej wcześniej.</span><span class="sxs-lookup"><span data-stu-id="0e471-241">Note how we used hello `--public-ip-name` switch toopass in hello `myPublicIP` that we created earlier.</span></span> <span data-ttu-id="0e471-242">Przypisywanie hello publicznego adresu IP usługi równoważenia obciążenia toohello adres pozwala tooreach maszyn wirtualnych między hello Internet.</span><span class="sxs-lookup"><span data-stu-id="0e471-242">Assigning hello public IP address toohello load balancer allows you tooreach your VMs across hello Internet.</span></span>

<span data-ttu-id="0e471-243">Następnie Utwórzmy naszych drugi pula IP teraz naszych ruchu zaplecza.</span><span class="sxs-lookup"><span data-stu-id="0e471-243">Next, let's create our second IP pool, this time for our back-end traffic.</span></span> <span data-ttu-id="0e471-244">Witaj poniższy przykład tworzy puli zaplecza, o nazwie `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="0e471-244">hello following example creates a back-end pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

<span data-ttu-id="0e471-245">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-245">Output:</span></span>

```azurecli
info:    Executing command network lb address-pool create
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

<span data-ttu-id="0e471-246">Zobaczysz, jak robi naszej usługi równoważenia obciążenia przez wyszukiwanie z `azure network lb show` i badanie danych wyjściowych JSON hello:</span><span class="sxs-lookup"><span data-stu-id="0e471-246">We can see how our load balancer is doing by looking with `azure network lb show` and examining hello JSON output:</span></span>

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

<span data-ttu-id="0e471-247">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-247">Output:</span></span>

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

## <a name="create-load-balancer-nat-rules"></a><span data-ttu-id="0e471-248">Tworzenie reguł NAT modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="0e471-248">Create load balancer NAT rules</span></span>
<span data-ttu-id="0e471-249">ruch tooget przepływających przez naszych modułu równoważenia obciążenia, potrzebujemy toocreate sieci adresu translacji adresów reguł określających działania ruchu przychodzącego lub wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="0e471-249">tooget traffic flowing through our load balancer, we need toocreate network address translation (NAT) rules that specify either inbound or outbound actions.</span></span> <span data-ttu-id="0e471-250">Należy określić hello toouse protokołu, a następnie mapują porty toointernal portów zewnętrznych zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="0e471-250">You can specify hello protocol toouse, then map external ports toointernal ports as desired.</span></span> <span data-ttu-id="0e471-251">W naszym środowisku Utwórzmy niektórych reguł, które umożliwiają SSH za pośrednictwem naszego tooour usługi równoważenia obciążenia maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="0e471-251">For our environment, let's create some rules that allow SSH through our load balancer tooour VMs.</span></span> <span data-ttu-id="0e471-252">Port TCP portów 4222 i 4223 toodirect tooTCP 22 skonfigurowanie na naszych maszyn wirtualnych (które możemy utworzyć później).</span><span class="sxs-lookup"><span data-stu-id="0e471-252">We set up TCP ports 4222 and 4223 toodirect tooTCP port 22 on our VMs (which we create later).</span></span> <span data-ttu-id="0e471-253">Witaj poniższy przykład powoduje utworzenie reguły o nazwie `myLoadBalancerRuleSSH1` toomap TCP port 4222 tooport 22:</span><span class="sxs-lookup"><span data-stu-id="0e471-253">hello following example creates a rule named `myLoadBalancerRuleSSH1` toomap TCP port 4222 tooport 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

<span data-ttu-id="0e471-254">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-254">Output:</span></span>

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up hello load balancer "myLoadBalancer"
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

<span data-ttu-id="0e471-255">Powtórz procedurę hello drugi reguły NAT dla SSH.</span><span class="sxs-lookup"><span data-stu-id="0e471-255">Repeat hello procedure for your second NAT rule for SSH.</span></span> <span data-ttu-id="0e471-256">Witaj poniższy przykład powoduje utworzenie reguły o nazwie `myLoadBalancerRuleSSH2` toomap TCP port 4223 tooport 22:</span><span class="sxs-lookup"><span data-stu-id="0e471-256">hello following example creates a rule named `myLoadBalancerRuleSSH2` toomap TCP port 4223 tooport 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

<span data-ttu-id="0e471-257">Umożliwia również Przejdź dalej i utworzyć regułę NAT dla portu TCP 80 dla ruchu w sieci web, Podłączanie reguły hello tooour pule adresów IP.</span><span class="sxs-lookup"><span data-stu-id="0e471-257">Let's also go ahead and create a NAT rule for TCP port 80 for web traffic, hooking hello rule up tooour IP pools.</span></span> <span data-ttu-id="0e471-258">Jeśli firma Microsoft dołączenie tooan reguły hello puli IP, a Podłączanie hello reguły tooour maszyny wirtualne pojedynczo, firma Microsoft można dodawać i usuwać maszyn wirtualnych z hello puli adresów IP.</span><span class="sxs-lookup"><span data-stu-id="0e471-258">If we hook up hello rule tooan IP pool, instead of hooking up hello rule tooour VMs individually, we can add or remove VMs from hello IP pool.</span></span> <span data-ttu-id="0e471-259">Moduł równoważenia obciążenia Hello automatycznie dostosowuje hello przepływu ruchu.</span><span class="sxs-lookup"><span data-stu-id="0e471-259">hello load balancer automatically adjusts hello flow of traffic.</span></span> <span data-ttu-id="0e471-260">Witaj poniższy przykład powoduje utworzenie reguły o nazwie `myLoadBalancerRuleWeb` toomap TCP port 80 tooport 80:</span><span class="sxs-lookup"><span data-stu-id="0e471-260">hello following example creates a rule named `myLoadBalancerRuleWeb` toomap TCP port 80 tooport 80:</span></span>

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

<span data-ttu-id="0e471-261">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-261">Output:</span></span>

```azurecli
info:    Executing command network lb rule create
+ Looking up hello load balancer "myLoadBalancer"
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

## <a name="create-a-load-balancer-health-probe"></a><span data-ttu-id="0e471-262">Utwórz kondycji sondę modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="0e471-262">Create a load balancer health probe</span></span>
<span data-ttu-id="0e471-263">Kondycję okresowo badania kontroli hello maszyn wirtualnych, które znajdują się za naszych się, że ich działania i odpowiada toorequests zgodnie z definicją toomake usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="0e471-263">A health probe periodically checks on hello VMs that are behind our load balancer toomake sure they're operating and responding toorequests as defined.</span></span> <span data-ttu-id="0e471-264">Jeśli nie są usuwane z tooensure operacji, które użytkownicy nie są kierowane toothem.</span><span class="sxs-lookup"><span data-stu-id="0e471-264">If not, they're removed from operation tooensure that users aren't being directed toothem.</span></span> <span data-ttu-id="0e471-265">Można zdefiniować niestandardowe sprawdza, czy hello sondy kondycji, oraz odstępach czasu i wartości limitu czasu.</span><span class="sxs-lookup"><span data-stu-id="0e471-265">You can define custom checks for hello health probe, along with intervals and timeout values.</span></span> <span data-ttu-id="0e471-266">Aby uzyskać więcej informacji na temat sondy kondycji, zobacz [sondy modułu równoważenia obciążenia](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0e471-266">For more information about health probes, see [Load Balancer probes](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="0e471-267">Witaj poniższy przykład tworzy TCP kondycji sondowany o nazwie `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="0e471-267">hello following example creates a TCP health probed named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

<span data-ttu-id="0e471-268">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-268">Output:</span></span>

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

<span data-ttu-id="0e471-269">W tym miejscu możemy określony interwał 15 sekund dla naszych kontroli kondycji.</span><span class="sxs-lookup"><span data-stu-id="0e471-269">Here, we specified an interval of 15 seconds for our health checks.</span></span> <span data-ttu-id="0e471-270">Firma Microsoft może pominąć maksymalnie cztery sond (jedną minutę), zanim hello modułu równoważenia obciążenia uzna, że nie działa na tym hoście hello.</span><span class="sxs-lookup"><span data-stu-id="0e471-270">We can miss a maximum of four probes (one minute) before hello load balancer considers that hello host is no longer functioning.</span></span>

## <a name="verify-hello-load-balancer"></a><span data-ttu-id="0e471-271">Sprawdź hello modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="0e471-271">Verify hello load balancer</span></span>
<span data-ttu-id="0e471-272">Po zakończeniu konfiguracji usługi równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="0e471-272">Now hello load balancer configuration is done.</span></span> <span data-ttu-id="0e471-273">Poniżej przedstawiono kroki hello, wykonane:</span><span class="sxs-lookup"><span data-stu-id="0e471-273">Here are hello steps you took:</span></span>

1. <span data-ttu-id="0e471-274">Utworzono usługę równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="0e471-274">You created a load balancer.</span></span>
2. <span data-ttu-id="0e471-275">Utworzyć pulę IP frontonu i przypisane publicznego tooit IP.</span><span class="sxs-lookup"><span data-stu-id="0e471-275">You created a front-end IP pool and assigned a public IP tooit.</span></span>
3. <span data-ttu-id="0e471-276">Została utworzona pula adresów IP zaplecza, która maszyny wirtualne mogą nawiązać połączenie.</span><span class="sxs-lookup"><span data-stu-id="0e471-276">You created a back-end IP pool that VMs can connect to.</span></span>
4. <span data-ttu-id="0e471-277">Utworzono reguł NAT, zezwalających na maszynach wirtualnych toohello SSH do zarządzania, oraz regułę zezwalającą port TCP 80 dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="0e471-277">You created NAT rules that allow SSH toohello VMs for management, along with a rule that allows TCP port 80 for our web app.</span></span>
5. <span data-ttu-id="0e471-278">Po dodaniu kondycji sondowania tooperiodically wyboru hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="0e471-278">You added a health probe tooperiodically check hello VMs.</span></span> <span data-ttu-id="0e471-279">Tej sondy kondycji gwarantuje, że użytkownicy nie próbują tooaccess maszynę Wirtualną, która jest już nie działa lub obsługę zawartości.</span><span class="sxs-lookup"><span data-stu-id="0e471-279">This health probe ensures that users don't try tooaccess a VM that is no longer functioning or serving content.</span></span>

<span data-ttu-id="0e471-280">Umożliwia przeglądanie jak teraz wygląda przez moduł równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="0e471-280">Let's review what your load balancer looks like now:</span></span>

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

<span data-ttu-id="0e471-281">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-281">Output:</span></span>

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

## <a name="create-an-nic-toouse-with-hello-linux-vm"></a><span data-ttu-id="0e471-282">Utwórz toouse karty Sieciowej z hello maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="0e471-282">Create an NIC toouse with hello Linux VM</span></span>
<span data-ttu-id="0e471-283">Karty sieciowe są programowo dostępne, ponieważ możesz zastosować zasady tootheir użycia.</span><span class="sxs-lookup"><span data-stu-id="0e471-283">NICs are programmatically available because you can apply rules tootheir use.</span></span> <span data-ttu-id="0e471-284">Może także zawierać więcej niż jeden.</span><span class="sxs-lookup"><span data-stu-id="0e471-284">You can also have more than one.</span></span> <span data-ttu-id="0e471-285">W następujących hello `azure network nic create` polecenia Podłączanie hello kart toohello obciążenia zaplecza puli adresów IP i powiązać ją z hello ruchu SSH toopermit reguły NAT.</span><span class="sxs-lookup"><span data-stu-id="0e471-285">In hello following `azure network nic create` command, you hook up hello NIC toohello load back-end IP pool and associate it with hello NAT rule toopermit SSH traffic.</span></span>

<span data-ttu-id="0e471-286">Zastąp hello `#####-###-###` sekcje z identyfikatorem subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0e471-286">Replace hello `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="0e471-287">Identyfikator jest odnotowany w danych wyjściowych hello subskrypcji `jq` podczas badania zasobów hello tworzenia.</span><span class="sxs-lookup"><span data-stu-id="0e471-287">Your subscription ID is noted in hello output of `jq` when you examine hello resources you are creating.</span></span> <span data-ttu-id="0e471-288">Można również wyświetlić identyfikator subskrypcji z `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="0e471-288">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="0e471-289">Witaj poniższy przykład tworzy karty Sieciowej o nazwie `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="0e471-289">hello following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

<span data-ttu-id="0e471-290">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-290">Output:</span></span>

```azurecli
info:    Executing command network nic create
+ Looking up hello subnet "mySubnet"
+ Looking up hello network interface "myNic1"
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

<span data-ttu-id="0e471-291">Można wyświetlić szczegóły hello, sprawdzając zasobów hello bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="0e471-291">You can see hello details by examining hello resource directly.</span></span> <span data-ttu-id="0e471-292">Należy zbadać hello zasobów za pomocą hello `azure network nic show` polecenia:</span><span class="sxs-lookup"><span data-stu-id="0e471-292">You examine hello resource by using hello `azure network nic show` command:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

<span data-ttu-id="0e471-293">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-293">Output:</span></span>

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

<span data-ttu-id="0e471-294">Teraz utworzymy hello drugiej karty Sieciowej, przechwytywanie w puli adresów IP zaplecza tooour ponownie.</span><span class="sxs-lookup"><span data-stu-id="0e471-294">Now we create hello second NIC, hooking in tooour back-end IP pool again.</span></span> <span data-ttu-id="0e471-295">Ta druga reguły NAT czasu hello zezwala na ruch protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="0e471-295">This time hello second NAT rule permits SSH traffic.</span></span> <span data-ttu-id="0e471-296">Witaj poniższy przykład tworzy karty Sieciowej o nazwie `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="0e471-296">hello following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a><span data-ttu-id="0e471-297">Utwórz grupę zabezpieczeń sieci i reguł</span><span class="sxs-lookup"><span data-stu-id="0e471-297">Create a network security group and rules</span></span>
<span data-ttu-id="0e471-298">Po wprowadzeniu Utwórz grupę zabezpieczeń sieci i hello reguły ruchu przychodzącego, które kontrolują dostęp toohello karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="0e471-298">Now we create a network security group and hello inbound rules that govern access toohello NIC.</span></span> <span data-ttu-id="0e471-299">Grupa zabezpieczeń sieci może być zastosowane tooa karty Sieciowej lub podsieci.</span><span class="sxs-lookup"><span data-stu-id="0e471-299">A network security group can be applied tooa NIC or subnet.</span></span> <span data-ttu-id="0e471-300">Należy zdefiniować reguły toocontrol hello przepływu ruchu do i z maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="0e471-300">You define rules toocontrol hello flow of traffic in and out of your VMs.</span></span> <span data-ttu-id="0e471-301">Witaj poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="0e471-301">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

<span data-ttu-id="0e471-302">Dodajmy hello regułę ruchu przychodzącego dla hello NSG tooallow przychodzących połączeń na porcie 22 (toosupport SSH).</span><span class="sxs-lookup"><span data-stu-id="0e471-302">Let's add hello inbound rule for hello NSG tooallow inbound connections on port 22 (toosupport SSH).</span></span> <span data-ttu-id="0e471-303">Witaj poniższy przykład powoduje utworzenie reguły o nazwie `myNetworkSecurityGroupRuleSSH` tooallow ruch TCP na porcie 22:</span><span class="sxs-lookup"><span data-stu-id="0e471-303">hello following example creates a rule named `myNetworkSecurityGroupRuleSSH` tooallow TCP on port 22:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

<span data-ttu-id="0e471-304">Teraz Dodajmy hello regułę ruchu przychodzącego dla hello NSG tooallow przychodzących połączeń na porcie 80 (toosupport ruchu w sieci web).</span><span class="sxs-lookup"><span data-stu-id="0e471-304">Now let's add hello inbound rule for hello NSG tooallow inbound connections on port 80 (toosupport web traffic).</span></span> <span data-ttu-id="0e471-305">Witaj poniższy przykład powoduje utworzenie reguły o nazwie `myNetworkSecurityGroupRuleHTTP` tooallow ruch TCP na porcie 80:</span><span class="sxs-lookup"><span data-stu-id="0e471-305">hello following example creates a rule named `myNetworkSecurityGroupRuleHTTP` tooallow TCP on port 80:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> <span data-ttu-id="0e471-306">reguły dla ruchu przychodzącego Hello jest filtrem dla połączeń sieciowych dla ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="0e471-306">hello inbound rule is a filter for inbound network connections.</span></span> <span data-ttu-id="0e471-307">W tym przykładzie mamy powiązać hello NSG toohello maszyn wirtualnych wirtualnej karty Sieciowej, co oznacza, że wszystkie żądania tooport 22 jest przekazywana toohello karty Sieciowej na naszych maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0e471-307">In this example, we bind hello NSG toohello VMs virtual NIC, which means that any request tooport 22 is passed through toohello NIC on our VM.</span></span> <span data-ttu-id="0e471-308">Tę regułę dla ruchu przychodzącego jest o połączenie sieciowe, a nie o punkt końcowy, który jest co byłoby o we wdrożeniach klasycznych.</span><span class="sxs-lookup"><span data-stu-id="0e471-308">This inbound rule is about a network connection, and not about an endpoint, which is what it would be about in classic deployments.</span></span> <span data-ttu-id="0e471-309">tooopen port musi pozostać hello `--source-port-range` ustawić także "\*" tooaccept (wartość domyślna hello) ruchu przychodzącego żądania od **żadnych** żąda portu.</span><span class="sxs-lookup"><span data-stu-id="0e471-309">tooopen a port, you must leave hello `--source-port-range` set too'\*' (hello default value) tooaccept inbound requests from **any** requesting port.</span></span> <span data-ttu-id="0e471-310">Porty są zwykle dynamiczne.</span><span class="sxs-lookup"><span data-stu-id="0e471-310">Ports are typically dynamic.</span></span>
>
>

## <a name="bind-toohello-nic"></a><span data-ttu-id="0e471-311">Powiąż toohello karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="0e471-311">Bind toohello NIC</span></span>
<span data-ttu-id="0e471-312">Powiąż hello NSG toohello kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="0e471-312">Bind hello NSG toohello NICs.</span></span> <span data-ttu-id="0e471-313">Potrzebujemy tooconnect naszych kart sieciowych z naszej grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="0e471-313">We need tooconnect our NICs with our network security group.</span></span> <span data-ttu-id="0e471-314">Uruchom zarówno polecenia toohook się naszego kart sieciowych:</span><span class="sxs-lookup"><span data-stu-id="0e471-314">Run both commands, toohook up both of our NICs:</span></span>

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a><span data-ttu-id="0e471-315">Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="0e471-315">Create an availability set</span></span>
<span data-ttu-id="0e471-316">Zestawy dostępności rozpowszechniania pomocy maszyn wirtualnych w domenach awarii i domen uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="0e471-316">Availability sets help spread your VMs across fault domains and upgrade domains.</span></span> <span data-ttu-id="0e471-317">Utwórz zbiór dostępności dla maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="0e471-317">Let's create an availability set for your VMs.</span></span> <span data-ttu-id="0e471-318">Witaj poniższy przykład tworzy zbiór nazwanego dostępności `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="0e471-318">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

<span data-ttu-id="0e471-319">Domen błędów Definiowanie grup maszyn wirtualnych, które współużytkują wspólne przełącznik źródła i sieci zasilania.</span><span class="sxs-lookup"><span data-stu-id="0e471-319">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="0e471-320">Domyślnie program hello maszyn wirtualnych, które są skonfigurowane w zestawie dostępności są rozdzielone przez się toothree domen błędów.</span><span class="sxs-lookup"><span data-stu-id="0e471-320">By default, hello virtual machines that are configured within your availability set are separated across up toothree fault domains.</span></span> <span data-ttu-id="0e471-321">pomysł Hello jest problemem sprzętowym w jednym z tych domen błędów nie wpływa na każdej maszynie Wirtualnej, która jest uruchomiona aplikacja.</span><span class="sxs-lookup"><span data-stu-id="0e471-321">hello idea is that a hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span> <span data-ttu-id="0e471-322">Azure automatycznie dystrybuuje maszyn wirtualnych w domenach awarii hello podczas umieszczania ich w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="0e471-322">Azure automatically distributes VMs across hello fault domains when placing them in an availability set.</span></span>

<span data-ttu-id="0e471-323">Domen uaktualnienia wskazują grupy maszyn wirtualnych i podstawowym sprzętem fizycznym, który może zostać uruchomiony ponownie na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="0e471-323">Upgrade domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="0e471-324">kolejność Hello, w którym są ponownie uruchamiane domen uaktualnienia może nie być sekwencyjnych podczas zaplanowanej konserwacji, ale tylko jedno uaktualnienie ponownego uruchomienia w czasie.</span><span class="sxs-lookup"><span data-stu-id="0e471-324">hello order in which upgrade domains are rebooted might not be sequential during planned maintenance, but only one upgrade is rebooted at a time.</span></span> <span data-ttu-id="0e471-325">Ponownie Azure automatycznie dystrybuuje maszyn wirtualnych między domenami uaktualnienia podczas umieszczania ich w witrynie dostępności.</span><span class="sxs-lookup"><span data-stu-id="0e471-325">Again, Azure automatically distributes your VMs across upgrade domains when placing them in an availability site.</span></span>

<span data-ttu-id="0e471-326">Przeczytaj więcej na temat [Zarządzanie hello dostępność maszyn wirtualnych](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0e471-326">Read more about [managing hello availability of VMs](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="create-hello-linux-vms"></a><span data-ttu-id="0e471-327">Tworzenie maszyn wirtualnych systemu Linux hello</span><span class="sxs-lookup"><span data-stu-id="0e471-327">Create hello Linux VMs</span></span>
<span data-ttu-id="0e471-328">Po utworzeniu hello zasobów magazynu i sieci maszyn wirtualnych toosupport dostępny z Internetu.</span><span class="sxs-lookup"><span data-stu-id="0e471-328">You've created hello storage and network resources toosupport Internet-accessible VMs.</span></span> <span data-ttu-id="0e471-329">Teraz załóżmy tworzenie tych maszyn wirtualnych i zabezpieczenia przy użyciu klucza SSH, który nie ma hasła.</span><span class="sxs-lookup"><span data-stu-id="0e471-329">Now let's create those VMs and secure them with an SSH key that doesn't have a password.</span></span> <span data-ttu-id="0e471-330">W takim przypadku zamierzamy toocreate maszyny Wirtualnej systemu Ubuntu oparte na powitania najnowszych LTS.</span><span class="sxs-lookup"><span data-stu-id="0e471-330">In this case, we're going toocreate an Ubuntu VM based on hello most recent LTS.</span></span> <span data-ttu-id="0e471-331">Możemy zlokalizować informacji obrazu przy użyciu `azure vm image list`, zgodnie z opisem w [znajdowanie obrazów maszyn wirtualnych Azure](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0e471-331">We locate that image information by using `azure vm image list`, as described in [finding Azure VM images](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="0e471-332">Wybraliśmy obrazu za pomocą polecenia hello `azure vm image list westeurope canonical | grep LTS`.</span><span class="sxs-lookup"><span data-stu-id="0e471-332">We selected an image by using hello command `azure vm image list westeurope canonical | grep LTS`.</span></span> <span data-ttu-id="0e471-333">W takim przypadku stosujemy `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span><span class="sxs-lookup"><span data-stu-id="0e471-333">In this case, we use `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span></span> <span data-ttu-id="0e471-334">Dla ostatniego pola hello jest przekazywana `latest` tak, aby w przyszłości hello zawsze uzyskujemy hello ostatniej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="0e471-334">For hello last field, we pass `latest` so that in hello future we always get hello most recent build.</span></span> <span data-ttu-id="0e471-335">(ciąg hello używamy jest `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span><span class="sxs-lookup"><span data-stu-id="0e471-335">(hello string we use is `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span></span>

<span data-ttu-id="0e471-336">Ten krok dalej jest znane tooanyone, który został już utworzony ssh publicznego i prywatnego klucza rsa pary w systemie Linux lub Mac za pomocą **ssh-keygen - t rsa -b 2048**.</span><span class="sxs-lookup"><span data-stu-id="0e471-336">This next step is familiar tooanyone who has already created an ssh rsa public and private key pair on Linux or Mac by using **ssh-keygen -t rsa -b 2048**.</span></span> <span data-ttu-id="0e471-337">Jeśli nie masz żadnych certyfikatów pary kluczy Twojej `~/.ssh` katalogu, można je utworzyć:</span><span class="sxs-lookup"><span data-stu-id="0e471-337">If you do not have any certificate key pairs in your `~/.ssh` directory, you can create them:</span></span>

* <span data-ttu-id="0e471-338">Automatycznie, przy użyciu hello `azure vm create --generate-ssh-keys` opcji.</span><span class="sxs-lookup"><span data-stu-id="0e471-338">Automatically, by using hello `azure vm create --generate-ssh-keys` option.</span></span>
* <span data-ttu-id="0e471-339">Ręcznie, używając [toocreate instrukcje hello je samodzielnie](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0e471-339">Manually, by using [hello instructions toocreate them yourself](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="0e471-340">Alternatywnie można użyć hello `--admin-password` tooauthenticate metody połączenia SSH po hello maszyny Wirtualnej jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="0e471-340">Alternatively, you can use hello `--admin-password` method tooauthenticate your SSH connections after hello VM is created.</span></span> <span data-ttu-id="0e471-341">Ta metoda jest zazwyczaj mniej bezpieczna.</span><span class="sxs-lookup"><span data-stu-id="0e471-341">This method is typically less secure.</span></span>

<span data-ttu-id="0e471-342">Utworzymy hello wirtualna przełączając naszych zasobów i informacji wraz z hello `azure vm create` polecenia:</span><span class="sxs-lookup"><span data-stu-id="0e471-342">We create hello VM by bringing all our resources and information together with hello `azure vm create` command:</span></span>

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

<span data-ttu-id="0e471-343">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-343">Output:</span></span>

```azurecli
info:    Executing command vm create
+ Looking up hello VM "myVM1"
info:    Verifying hello public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using hello VM Size "Standard_DS1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Looking up hello storage account mystorageaccount
+ Looking up hello availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up hello NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in hello NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    hello storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by hello parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

<span data-ttu-id="0e471-344">Możesz połączyć natychmiast tooyour maszyny Wirtualnej przy użyciu kluczy SSH domyślne.</span><span class="sxs-lookup"><span data-stu-id="0e471-344">You can connect tooyour VM immediately by using your default SSH keys.</span></span> <span data-ttu-id="0e471-345">Upewnij się, określ odpowiedni port hello, ponieważ firma Microsoft jest przekazanie za pośrednictwem usługi równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="0e471-345">Make sure that you specify hello appropriate port since we're passing through hello load balancer.</span></span> <span data-ttu-id="0e471-346">(Dla naszych pierwsza maszyna wirtualna, możemy skonfigurować hello NAT reguły tooforward portu 4222 tooour maszyny Wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="0e471-346">(For our first VM, we set up hello NAT rule tooforward port 4222 tooour VM.)</span></span>

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

<span data-ttu-id="0e471-347">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-347">Output:</span></span>

```bash
hello authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

<span data-ttu-id="0e471-348">Przejdź dalej i utworzyć drugi maszyny Wirtualnej w hello tak samo jak:</span><span class="sxs-lookup"><span data-stu-id="0e471-348">Go ahead and create your second VM in hello same manner:</span></span>

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

<span data-ttu-id="0e471-349">I można teraz używać hello `azure vm show myResourceGroup myVM1` polecenia tooexamine został utworzony.</span><span class="sxs-lookup"><span data-stu-id="0e471-349">And you can now use hello `azure vm show myResourceGroup myVM1` command tooexamine what you've created.</span></span> <span data-ttu-id="0e471-350">W tym momencie używasz Ubuntu maszyn wirtualnych za modułem równoważenia obciążenia w Azure, który użytkownik może zalogować się do tylko z Twojej pary kluczy SSH (ponieważ haseł są wyłączone).</span><span class="sxs-lookup"><span data-stu-id="0e471-350">At this point, you're running your Ubuntu VMs behind a load balancer in Azure that you can sign into only with your SSH key pair (because passwords are disabled).</span></span> <span data-ttu-id="0e471-351">Można zainstalować nginx lub host z wieloma adresami, wdrażanie aplikacji sieci web i widoczny ruch hello przepływ przez tooboth usługi równoważenia obciążenia hello hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="0e471-351">You can install nginx or httpd, deploy a web app, and see hello traffic flow through hello load balancer tooboth of hello VMs.</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

<span data-ttu-id="0e471-352">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0e471-352">Output:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up hello VM "TestVM1"
+ Looking up hello NIC "myNic1"
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


## <a name="export-hello-environment-as-a-template"></a><span data-ttu-id="0e471-353">Eksportuj środowiska hello jako szablon</span><span class="sxs-lookup"><span data-stu-id="0e471-353">Export hello environment as a template</span></span>
<span data-ttu-id="0e471-354">Teraz, to środowisko, co zrobić, jeśli chcesz toocreate mają wbudowane dodatkowe środowiska hello takie same parametry lub w środowisku produkcyjnym, odpowiadający jej?</span><span class="sxs-lookup"><span data-stu-id="0e471-354">Now that you have built out this environment, what if you want toocreate an additional development environment with hello same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="0e471-355">Menedżer zasobów używa szablony JSON, definiują wszystkie parametry hello w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="0e471-355">Resource Manager uses JSON templates that define all hello parameters for your environment.</span></span> <span data-ttu-id="0e471-356">Limit całego środowiska kompilacji, umieszczając odwołanie do tego szablonu JSON.</span><span class="sxs-lookup"><span data-stu-id="0e471-356">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="0e471-357">Możesz [ręcznie utworzyć szablony JSON](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub wyeksportować istniejącego środowiska toocreate hello JSON szablonu dla Ciebie:</span><span class="sxs-lookup"><span data-stu-id="0e471-357">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment toocreate hello JSON template for you:</span></span>

```azurecli
azure group export --name myResourceGroup
```

<span data-ttu-id="0e471-358">To polecenie tworzy hello `myResourceGroup.json` plik w bieżącym katalogu roboczym.</span><span class="sxs-lookup"><span data-stu-id="0e471-358">This command creates hello `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="0e471-359">Podczas tworzenia środowiska z tego szablonu, wyświetlany jest monit dla wszystkich nazw zasobów hello, w tym nazwy hello hello modułu równoważenia obciążenia, interfejsów sieciowych lub maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="0e471-359">When you create an environment from this template, you are prompted for all hello resource names, including hello names for hello load balancer, network interfaces, or VMs.</span></span> <span data-ttu-id="0e471-360">Można go wypełnić te nazwy w pliku szablonu, dodając hello `-p` lub `--includeParameterDefaultValue` toohello parametru `azure group export` polecenia, która została przedstawiona wcześniej.</span><span class="sxs-lookup"><span data-stu-id="0e471-360">You can populate these names in your template file by adding hello `-p` or `--includeParameterDefaultValue` parameter toohello `azure group export` command that was shown earlier.</span></span> <span data-ttu-id="0e471-361">Edytowanie nazwy JSON szablonu toospecify hello zasobów lub [Tworzenie pliku parameters.JSON następującym kodem](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) określający hello nazw zasobów.</span><span class="sxs-lookup"><span data-stu-id="0e471-361">Edit your JSON template toospecify hello resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies hello resource names.</span></span>

<span data-ttu-id="0e471-362">toocreate środowisko z szablonu:</span><span class="sxs-lookup"><span data-stu-id="0e471-362">toocreate an environment from your template:</span></span>

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

<span data-ttu-id="0e471-363">Może być tooread [więcej informacji na temat toodeploy z szablonów](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0e471-363">You might want tooread [more about how toodeploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="0e471-364">Więcej informacji na temat jak tooincrementally środowisk aktualizacji, użyj pliku parametrów hello i uzyskiwać dostęp do szablonów z lokalizacji magazynu jednego.</span><span class="sxs-lookup"><span data-stu-id="0e471-364">Learn about how tooincrementally update environments, use hello parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e471-365">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0e471-365">Next steps</span></span>
<span data-ttu-id="0e471-366">Teraz wszystko jest gotowe toobegin Praca z wielu składników sieciowych i maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="0e471-366">Now you're ready toobegin working with multiple networking components and VMs.</span></span> <span data-ttu-id="0e471-367">Za pomocą hello podstawowe składniki wprowadzone w tym miejscu, można użyć tej próbki toobuild środowiska limit aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0e471-367">You can use this sample environment toobuild out your application by using hello core components introduced here.</span></span>
