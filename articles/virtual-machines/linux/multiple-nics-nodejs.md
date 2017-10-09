---
title: "aaaCreate Maszynę wirtualną systemu Linux na platformie Azure z wieloma kartami sieciowymi | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Maszynę wirtualną systemu Linux z wieloma kartami sieciowymi dołączony tooit za pomocą szablonów hello Azure CLI lub Menedżera zasobów."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 457dab734ceeeefd35cddaf1ebb9ea0a82f4e207
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="1ac3f-103">Utwórz maszynę wirtualną systemu Linux z wieloma kartami sieciowymi przy użyciu hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="1ac3f-103">Create a Linux virtual machine with multiple NICs using hello Azure CLI 1.0</span></span>
<span data-ttu-id="1ac3f-104">Można utworzyć maszynę wirtualną (VM) na platformie Azure, który ma wiele tooit interfejsów (NIC), podłączonych sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached tooit.</span></span> <span data-ttu-id="1ac3f-105">Typowy scenariusz obejmuje toohave w różnych podsieciach łączności frontonu i zaplecza, lub sieci dedykowanej tooa monitorowania lub tworzenia kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="1ac3f-106">Ten artykuł zawiera toocreate szybkie polecenia maszyny Wirtualnej z wielu kart sieciowych dołączonych tooit.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-106">This article provides quick commands toocreate a VM with multiple NICs attached tooit.</span></span> <span data-ttu-id="1ac3f-107">Aby uzyskać szczegółowe informacje, w tym jak toocreate wiele kart sieciowych w ramach własnego Bash skrypty, przeczytaj więcej na temat [wdrażanie maszyn wirtualnych z wieloma kartami Sieciowymi](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="1ac3f-107">For detailed information, including how toocreate multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="1ac3f-108">Różne [rozmiarów maszyn wirtualnych](sizes.md) obsługuje różną liczbę kart sieciowych, więc odpowiednio rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

> [!WARNING]
> <span data-ttu-id="1ac3f-109">Podczas tworzenia maszyny Wirtualnej — nie można dodać istniejącej maszyny Wirtualnej z hello Azure CLI 1.0 tooan kart sieciowych należy dołączyć wiele kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-109">You must attach multiple NICs when you create a VM - you cannot add NICs tooan existing VM with hello Azure CLI 1.0.</span></span> <span data-ttu-id="1ac3f-110">Możesz [dodać tooan kart sieciowych z istniejącej maszyny Wirtualnej z hello Azure CLI 2.0](multiple-nics.md).</span><span class="sxs-lookup"><span data-stu-id="1ac3f-110">You can [add NICs tooan existing VM with hello Azure CLI 2.0](multiple-nics.md).</span></span> <span data-ttu-id="1ac3f-111">Możesz również [Utwórz maszynę Wirtualną, oparte na dyskach wirtualnych oryginalnego hello](copy-vm.md) i utworzyć wiele kart sieciowych, jak wdrożyć hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-111">You can also [create a VM based on hello original virtual disk(s)](copy-vm.md) and create multiple NICs as you deploy hello VM.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="1ac3f-112">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="1ac3f-112">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="1ac3f-113">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="1ac3f-113">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="1ac3f-114">[Azure CLI 1.0](#create-supporting-resources) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="1ac3f-114">[Azure CLI 1.0](#create-supporting-resources) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="1ac3f-115">[Azure CLI 2.0](multiple-nics.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="1ac3f-115">[Azure CLI 2.0](multiple-nics.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="1ac3f-116">Utwórz dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="1ac3f-116">Create supporting resources</span></span>
<span data-ttu-id="1ac3f-117">Upewnij się, że masz hello [interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md) zalogowany i w trybie Menedżera zasobów:</span><span class="sxs-lookup"><span data-stu-id="1ac3f-117">Make sure that you have hello [Azure CLI](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="1ac3f-118">Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-118">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="1ac3f-119">Przykład nazwy parametrów uwzględnione *myResourceGroup*, *mojekontomagazynu*, i *myVM*.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-119">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="1ac3f-120">Najpierw utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-120">First, create a resource group.</span></span> <span data-ttu-id="1ac3f-121">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="1ac3f-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

<span data-ttu-id="1ac3f-122">Utwórz toohold konta magazynu maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-122">Create a storage account toohold your VMs.</span></span> <span data-ttu-id="1ac3f-123">Witaj poniższy przykład tworzy konto magazynu o nazwie *mojekontomagazynu*:</span><span class="sxs-lookup"><span data-stu-id="1ac3f-123">hello following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

<span data-ttu-id="1ac3f-124">Tworzenie maszyn wirtualnych do tooconnect sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-124">Create a virtual network tooconnect your VMs to.</span></span> <span data-ttu-id="1ac3f-125">Witaj poniższy przykład tworzy sieć wirtualną o nazwie *myVnet* z prefiksem adresu o *192.168.0.0/16*:</span><span class="sxs-lookup"><span data-stu-id="1ac3f-125">hello following example creates a virtual network named *myVnet* with an address prefix of *192.168.0.0/16*:</span></span>

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="1ac3f-126">Utwórz dwie sieci wirtualnej podsieci — po jednej dla ruchu frontonu i jedną dla ruchu zaplecza.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-126">Create two virtual network subnets - one for front-end traffic and one for back-end traffic.</span></span> <span data-ttu-id="1ac3f-127">Witaj poniższy przykład tworzy dwie podsieci o nazwie *mySubnetFrontEnd* i *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="1ac3f-127">hello following example creates two subnets, named *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

```azurecli
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetFrontEnd \
    --address-prefix 192.168.1.0/24
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="1ac3f-128">Tworzenie i konfigurowanie wielu kart sieciowych</span><span class="sxs-lookup"><span data-stu-id="1ac3f-128">Create and configure multiple NICs</span></span>
<span data-ttu-id="1ac3f-129">Więcej informacji zawiera temat [wdrażania wielu kart sieciowych przy użyciu interfejsu wiersza polecenia Azure hello](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), tym skrypty proces hello wszystkich kart hello toocreate w pętli.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-129">You can read more details about [deploying multiple NICs using hello Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), including scripting hello process of looping through toocreate all hello NICs.</span></span>

<span data-ttu-id="1ac3f-130">Witaj poniższy przykład tworzy dwie karty sieciowe, o nazwie *myNic1* i *myNic2*, z jedną kartą Sieciową łączące tooeach podsieci:</span><span class="sxs-lookup"><span data-stu-id="1ac3f-130">hello following example creates two NICs, named *myNic1* and *myNic2*, with one NIC connecting tooeach subnet:</span></span>

```azurecli
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic1 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetFrontEnd
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic2 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetBackEnd
```

<span data-ttu-id="1ac3f-131">Zwykle również utworzyć [sieciowej grupy zabezpieczeń](../../virtual-network/virtual-networks-nsg.md) lub [modułu równoważenia obciążenia](../../load-balancer/load-balancer-overview.md) toohelp zarządzania i rozpowszechniają ruch maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-131">Typically you also create a [Network Security Group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) toohelp manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="1ac3f-132">Witaj poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="1ac3f-132">hello following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="1ac3f-133">Powiąż z kart sieciowych toohello grupy zabezpieczeń sieci przy użyciu `azure network nic set`.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-133">Bind your NICs toohello Network Security Group using `azure network nic set`.</span></span> <span data-ttu-id="1ac3f-134">Witaj poniższy przykład wiąże *myNic1* i *myNic2* z *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="1ac3f-134">hello following example binds *myNic1* and *myNic2* with *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic1 \
    --network-security-group-name myNetworkSecurityGroup
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic2 \
    --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a><span data-ttu-id="1ac3f-135">Utwórz Maszynę wirtualną i Dołącz hello kart sieciowych</span><span class="sxs-lookup"><span data-stu-id="1ac3f-135">Create a VM and attach hello NICs</span></span>
<span data-ttu-id="1ac3f-136">Podczas tworzenia hello maszyny Wirtualnej, teraz należy określić wiele kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-136">When creating hello VM, you now specify multiple NICs.</span></span> <span data-ttu-id="1ac3f-137">Zamiast przy użyciu `--nic-name` tooprovide jedną kartę Sieciową, zamiast tego należy użyć `--nic-names` i zawierają rozdzielaną przecinkami listę kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-137">Rather using `--nic-name` tooprovide a single NIC, instead you use `--nic-names` and provide a comma-separated list of NICs.</span></span> <span data-ttu-id="1ac3f-138">Należy również uwagę tootake po wybraniu hello rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-138">You also need tootake care when you select hello VM size.</span></span> <span data-ttu-id="1ac3f-139">Istnieją ograniczenia hello całkowitą liczbę kart sieciowych, że można dodawać tooa maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-139">There are limits for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="1ac3f-140">Przeczytaj więcej na temat [rozmiarów maszyn wirtualnych systemu Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="1ac3f-140">Read more about [Linux VM sizes](sizes.md).</span></span> <span data-ttu-id="1ac3f-141">Witaj poniższy przykład przedstawia sposób toospecify wiele kart sieciowych, a następnie maszyny Wirtualnej rozmiaru obsługującego przy użyciu wielu kart sieciowych (*Standard_DS2_v2*):</span><span class="sxs-lookup"><span data-stu-id="1ac3f-141">hello following example shows how toospecify multiple NICs and then a VM size that supports using multiple NICs (*Standard_DS2_v2*):</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --os-type linux \
    --nic-names myNic1,myNic2 \
    --vm-size Standard_DS2_v2 \
    --storage-account-name mystorageaccount \
    --image-urn UbuntuLTS \
    --admin-username azureuser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub
```

## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="1ac3f-142">Tworzenie wielu kart sieciowych przy użyciu szablonów usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1ac3f-142">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="1ac3f-143">Szablony usługi Azure Resource Manager Użyj deklaratywne toodefine pliki JSON środowiska.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-143">Azure Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="1ac3f-144">Możesz przeczytać [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1ac3f-144">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="1ac3f-145">Szablony Menedżera zasobów zapewniają toocreate sposób wielu wystąpień zasobu podczas wdrażania, takich jak tworzenie wielu kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-145">Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="1ac3f-146">Możesz użyć *kopiowania* toospecify hello liczbę wystąpień toocreate:</span><span class="sxs-lookup"><span data-stu-id="1ac3f-146">You use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="1ac3f-147">Przeczytaj więcej na temat [tworzenia wielu wystąpień przy użyciu *kopiowania*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="1ac3f-147">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="1ac3f-148">Można również użyć `copyIndex()` toothen append numer Nazwa zasobu tooa, dzięki czemu można toocreate `myNic1`, `myNic2`, itp. hello poniżej pokazano przykład dołączanie wartość indeksu hello:</span><span class="sxs-lookup"><span data-stu-id="1ac3f-148">You can also use a `copyIndex()` toothen append a number tooa resource name, which allows you toocreate `myNic1`, `myNic2`, etc. hello following shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="1ac3f-149">Pełny przykład można znaleźć [tworzenia wielu kart sieciowych przy użyciu szablonów usługi Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="1ac3f-149">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ac3f-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1ac3f-150">Next steps</span></span>
<span data-ttu-id="1ac3f-151">Upewnij się, że tooreview [rozmiarów maszyn wirtualnych systemu Linux](sizes.md) podczas próby toocreating Maszynę wirtualną z wieloma kartami sieciowymi.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-151">Make sure tooreview [Linux VM sizes](sizes.md) when trying toocreating a VM with multiple NICs.</span></span> <span data-ttu-id="1ac3f-152">Należy zwrócić uwagę toohello maksymalną liczbę kart sieciowych obsługuje każdego rozmiaru maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-152">Pay attention toohello maximum number of NICs each VM size supports.</span></span> 

<span data-ttu-id="1ac3f-153">Należy pamiętać, że nie można dodać dodatkowe tooan kart sieciowych, istniejącej maszyny Wirtualnej, należy utworzyć wszystkich kart hello podczas wdrażania hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-153">Remember that you cannot add additional NICs tooan existing VM, you must create all hello NICs when you deploy hello VM.</span></span> <span data-ttu-id="1ac3f-154">Zachowaj ostrożność podczas planowania Twojej się, że wszystkie wymagane hello połączenia sieciowego z początku hello toomake wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="1ac3f-154">Take care when planning your deployments toomake sure that you have all hello required network connectivity from hello outset.</span></span>

