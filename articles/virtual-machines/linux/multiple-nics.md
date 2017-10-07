---
title: "aaaCreate Maszynę wirtualną systemu Linux na platformie Azure z wieloma kartami sieciowymi | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Maszynę wirtualną systemu Linux z wieloma kartami sieciowymi dołączony tooit za pomocą szablonów hello Azure CLI w wersji 2.0 lub Menedżera zasobów."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 5d2d04d0-fc62-45fa-88b1-61808a2bc691
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2723405914777a5dce4354d4f5d8413e357f58e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a><span data-ttu-id="70b70-103">Jak kartami interfejsu toocreate maszyny wirtualnej systemu Linux na platformie Azure z wielu sieci</span><span class="sxs-lookup"><span data-stu-id="70b70-103">How toocreate a Linux virtual machine in Azure with multiple network interface cards</span></span>
<span data-ttu-id="70b70-104">Można utworzyć maszynę wirtualną (VM) na platformie Azure, który ma wiele tooit interfejsów (NIC), podłączonych sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="70b70-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached tooit.</span></span> <span data-ttu-id="70b70-105">Typowy scenariusz obejmuje toohave w różnych podsieciach łączności frontonu i zaplecza, lub sieci dedykowanej tooa monitorowania lub tworzenia kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="70b70-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="70b70-106">W tym artykule szczegółowo jak tooit dołączony toocreate Maszynę wirtualną z wieloma kartami sieciowymi i jak tooadd lub usuń karty sieciowe z istniejącej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="70b70-106">This article details how toocreate a VM with multiple NICs attached tooit and how tooadd or remove NICs from an existing VM.</span></span> <span data-ttu-id="70b70-107">Aby uzyskać szczegółowe informacje, w tym jak toocreate wiele kart sieciowych w ramach własnego Bash skrypty, przeczytaj więcej na temat [wdrażanie maszyn wirtualnych z wieloma kartami Sieciowymi](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="70b70-107">For detailed information, including how toocreate multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="70b70-108">Różne [rozmiarów maszyn wirtualnych](sizes.md) obsługuje różną liczbę kart sieciowych, więc odpowiednio rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="70b70-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="70b70-109">Ten artykuł zawiera szczegóły dotyczące sposobu toocreate a maszyn wirtualnych z wieloma kartami sieciowymi z hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="70b70-109">This article details how toocreate a VM with multiple NICs with hello Azure CLI 2.0.</span></span> <span data-ttu-id="70b70-110">Można również wykonać te kroki hello [Azure CLI 1.0](multiple-nics-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="70b70-110">You can also perform these steps with hello [Azure CLI 1.0](multiple-nics-nodejs.md).</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="70b70-111">Utwórz dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="70b70-111">Create supporting resources</span></span>
<span data-ttu-id="70b70-112">Najnowsza wersja hello instalacji [Azure CLI 2.0](/cli/azure/install-az-cli2) i zaloguj się za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="70b70-112">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="70b70-113">Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="70b70-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="70b70-114">Przykład nazwy parametrów uwzględnione *myResourceGroup*, *mojekontomagazynu*, i *myVM*.</span><span class="sxs-lookup"><span data-stu-id="70b70-114">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="70b70-115">Najpierw utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="70b70-115">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="70b70-116">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="70b70-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="70b70-117">Utwórz sieć wirtualną hello z [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="70b70-117">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="70b70-118">Witaj poniższy przykład tworzy sieć wirtualną o nazwie *myVnet* i podsieć o nazwie *mySubnetFrontEnd*:</span><span class="sxs-lookup"><span data-stu-id="70b70-118">hello following example creates a virtual network named *myVnet* and subnet named *mySubnetFrontEnd*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="70b70-119">Utwórz podsieć dla ruchu zaplecza hello z [Utwórz podsieć sieci wirtualnej sieci az](/cli/azure/network/vnet/subnet#create).</span><span class="sxs-lookup"><span data-stu-id="70b70-119">Create a subnet for hello back-end traffic with [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span></span> <span data-ttu-id="70b70-120">Witaj poniższy przykład tworzy podsieć o nazwie *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="70b70-120">hello following example creates a subnet named *mySubnetBackEnd*:</span></span>

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

<span data-ttu-id="70b70-121">Utwórz grupę zabezpieczeń sieci z [utworzyć nsg sieci az](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="70b70-121">Create a network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="70b70-122">Witaj poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="70b70-122">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="70b70-123">Tworzenie i konfigurowanie wielu kart sieciowych</span><span class="sxs-lookup"><span data-stu-id="70b70-123">Create and configure multiple NICs</span></span>
<span data-ttu-id="70b70-124">Utwórz dwie karty sieciowe z [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="70b70-124">Create two NICs with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="70b70-125">Witaj poniższy przykład tworzy dwie karty sieciowe, o nazwie *myNic1* i *myNic2*, połączonych hello grupy zabezpieczeń sieci, z jedną kartą Sieciową łączące tooeach podsieci:</span><span class="sxs-lookup"><span data-stu-id="70b70-125">hello following example creates two NICs, named *myNic1* and *myNic2*, connected hello network security group, with one NIC connecting tooeach subnet:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic1 \
    --vnet-name myVnet \
    --subnet mySubnetFrontEnd \
    --network-security-group myNetworkSecurityGroup
az network nic create \
    --resource-group myResourceGroup \
    --name myNic2 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a><span data-ttu-id="70b70-126">Utwórz Maszynę wirtualną i Dołącz hello kart sieciowych</span><span class="sxs-lookup"><span data-stu-id="70b70-126">Create a VM and attach hello NICs</span></span>
<span data-ttu-id="70b70-127">Podczas tworzenia hello maszyny Wirtualnej, określ hello karty sieciowe zostały utworzone z `--nics`.</span><span class="sxs-lookup"><span data-stu-id="70b70-127">When you create hello VM, specify hello NICs you created with `--nics`.</span></span> <span data-ttu-id="70b70-128">Należy również uwagę tootake po wybraniu hello rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="70b70-128">You also need tootake care when you select hello VM size.</span></span> <span data-ttu-id="70b70-129">Istnieją ograniczenia hello całkowitą liczbę kart sieciowych, że można dodawać tooa maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="70b70-129">There are limits for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="70b70-130">Przeczytaj więcej na temat [rozmiarów maszyn wirtualnych systemu Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="70b70-130">Read more about [Linux VM sizes](sizes.md).</span></span> 

<span data-ttu-id="70b70-131">Utwórz maszynę wirtualną za pomocą polecenia [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="70b70-131">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="70b70-132">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM*:</span><span class="sxs-lookup"><span data-stu-id="70b70-132">hello following example creates a VM named *myVM*:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --size Standard_DS3_v2 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic1 myNic2
```

## <a name="add-a-nic-tooa-vm"></a><span data-ttu-id="70b70-133">Dodaj tooa karty Sieciowej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="70b70-133">Add a NIC tooa VM</span></span>
<span data-ttu-id="70b70-134">poprzednie kroki Hello utworzyć Maszynę wirtualną z wieloma kartami sieciowymi.</span><span class="sxs-lookup"><span data-stu-id="70b70-134">hello previous steps created a VM with multiple NICs.</span></span> <span data-ttu-id="70b70-135">Można również dodać istniejące maszyny Wirtualnej z hello Azure CLI 2.0 tooan kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="70b70-135">You can also add NICs tooan existing VM with hello Azure CLI 2.0.</span></span> 

<span data-ttu-id="70b70-136">Utwórz inną kartą Sieciową o [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="70b70-136">Create another NIC with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="70b70-137">Witaj poniższy przykład tworzy karty Sieciowej o nazwie *myNic3* podłączone podsieci wewnętrznej toohello i grupy zabezpieczeń sieci utworzone w poprzednich krokach hello:</span><span class="sxs-lookup"><span data-stu-id="70b70-137">hello following example creates a NIC named *myNic3* connected toohello back-end subnet and network security group created in hello previous steps:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="70b70-138">tooadd tooan kart istniejącej maszyny Wirtualnej, najpierw cofnąć hello maszyny Wirtualnej z [deallocate wirtualna az](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="70b70-138">tooadd a NIC tooan existing VM, first deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="70b70-139">Witaj poniższy przykład cofa alokację hello maszyny Wirtualnej o nazwie *myVM*:</span><span class="sxs-lookup"><span data-stu-id="70b70-139">hello following example deallocates hello VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="70b70-140">Dodaj hello kartą Sieciową o [Dodaj kartę sieciową maszyny wirtualnej az](/cli/azure/vm/nic#add).</span><span class="sxs-lookup"><span data-stu-id="70b70-140">Add hello NIC with [az vm nic add](/cli/azure/vm/nic#add).</span></span> <span data-ttu-id="70b70-141">Witaj poniższy przykład umożliwia dodanie *myNic3* za*myVM*:</span><span class="sxs-lookup"><span data-stu-id="70b70-141">hello following example adds *myNic3* too*myVM*:</span></span>

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

<span data-ttu-id="70b70-142">Uruchom hello maszyny Wirtualnej z [uruchomienia maszyny wirtualnej az](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="70b70-142">Start hello VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a><span data-ttu-id="70b70-143">Usuń kartę Sieciową z maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="70b70-143">Remove a NIC from a VM</span></span>
<span data-ttu-id="70b70-144">tooremove karty Sieciowej z istniejącej maszyny Wirtualnej, najpierw cofnąć hello maszyny Wirtualnej z [deallocate wirtualna az](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="70b70-144">tooremove a NIC from an existing VM, first deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="70b70-145">Witaj poniższy przykład cofa alokację hello maszyny Wirtualnej o nazwie *myVM*:</span><span class="sxs-lookup"><span data-stu-id="70b70-145">hello following example deallocates hello VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="70b70-146">Usuń hello kartą Sieciową o [Usuń kartę sieciową maszyny wirtualnej az](/cli/azure/vm/nic#remove).</span><span class="sxs-lookup"><span data-stu-id="70b70-146">Remove hello NIC with [az vm nic remove](/cli/azure/vm/nic#remove).</span></span> <span data-ttu-id="70b70-147">Witaj poniższy przykład umożliwia usunięcie *myNic3* z *myVM*:</span><span class="sxs-lookup"><span data-stu-id="70b70-147">hello following example removes *myNic3* from *myVM*:</span></span>

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

<span data-ttu-id="70b70-148">Uruchom hello maszyny Wirtualnej z [uruchomienia maszyny wirtualnej az](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="70b70-148">Start hello VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="70b70-149">Tworzenie wielu kart sieciowych przy użyciu szablonów usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="70b70-149">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="70b70-150">Szablony usługi Azure Resource Manager Użyj deklaratywne toodefine pliki JSON środowiska.</span><span class="sxs-lookup"><span data-stu-id="70b70-150">Azure Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="70b70-151">Możesz przeczytać [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="70b70-151">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="70b70-152">Szablony Menedżera zasobów zapewniają toocreate sposób wielu wystąpień zasobu podczas wdrażania, takich jak tworzenie wielu kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="70b70-152">Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="70b70-153">Możesz użyć *kopiowania* toospecify hello liczbę wystąpień toocreate:</span><span class="sxs-lookup"><span data-stu-id="70b70-153">You use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="70b70-154">Przeczytaj więcej na temat [tworzenia wielu wystąpień przy użyciu *kopiowania*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="70b70-154">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="70b70-155">Można również użyć `copyIndex()` toothen append numer Nazwa zasobu tooa, dzięki czemu można toocreate `myNic1`, `myNic2`, itp. hello poniżej pokazano przykład dołączanie wartość indeksu hello:</span><span class="sxs-lookup"><span data-stu-id="70b70-155">You can also use a `copyIndex()` toothen append a number tooa resource name, which allows you toocreate `myNic1`, `myNic2`, etc. hello following shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="70b70-156">Pełny przykład można znaleźć [tworzenia wielu kart sieciowych przy użyciu szablonów usługi Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="70b70-156">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="70b70-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="70b70-157">Next steps</span></span>
<span data-ttu-id="70b70-158">Przegląd [rozmiarów maszyn wirtualnych systemu Linux](sizes.md) podczas próby toocreating Maszynę wirtualną z wieloma kartami sieciowymi.</span><span class="sxs-lookup"><span data-stu-id="70b70-158">Review [Linux VM sizes](sizes.md) when trying toocreating a VM with multiple NICs.</span></span> <span data-ttu-id="70b70-159">Należy zwrócić uwagę toohello maksymalną liczbę kart sieciowych obsługuje każdego rozmiaru maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="70b70-159">Pay attention toohello maximum number of NICs each VM size supports.</span></span> 
