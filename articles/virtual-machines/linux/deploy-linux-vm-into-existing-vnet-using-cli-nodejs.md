---
title: "aaaDeploy maszyn wirtualnych systemu Linux w istniejącej sieci z interfejsu wiersza polecenia platformy Azure w wersji 1.0 | Dokumentacja firmy Microsoft"
description: "Jak toodeploy Maszynę wirtualną systemu Linux w istniejącej sieci wirtualnej przy użyciu hello Azure CLI w wersji 1.0"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e660f1563d386efc7788bd236f8b067145ea09bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli-10"></a><span data-ttu-id="34c1a-103">Jak toodeploy maszyny wirtualnej systemu Linux w istniejącej sieci wirtualnej platformy Azure z hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="34c1a-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure CLI 1.0</span></span>

<span data-ttu-id="34c1a-104">W tym artykule opisano sposób toodeploy toouse Azure CLI 1.0 maszynę wirtualną (VM) do istniejącej sieci wirtualnej (VNet).</span><span class="sxs-lookup"><span data-stu-id="34c1a-104">This article shows you how toouse Azure CLI 1.0 toodeploy a virtual machine (VM) into an existing Virtual Network (VNet).</span></span> <span data-ttu-id="34c1a-105">wymagania dotyczące Hello są:</span><span class="sxs-lookup"><span data-stu-id="34c1a-105">hello requirements are:</span></span>

- [<span data-ttu-id="34c1a-106">Konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="34c1a-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="34c1a-107">Pliki kluczy publicznych i prywatnych SSH</span><span class="sxs-lookup"><span data-stu-id="34c1a-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="34c1a-108">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="34c1a-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="34c1a-109">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="34c1a-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="34c1a-110">[Azure CLI 1.0](#quick-commands) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="34c1a-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="34c1a-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="34c1a-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="34c1a-112">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="34c1a-112">Quick Commands</span></span>

<span data-ttu-id="34c1a-113">Jeśli potrzebujesz tooquickly hello zadania, powitania po sekcji Szczegóły poleceń hello potrzebne.</span><span class="sxs-lookup"><span data-stu-id="34c1a-113">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="34c1a-114">Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć hello pozostałej części dokumentu hello [uruchamiania tutaj](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="34c1a-114">More detailed information and context for each step can be found hello rest of hello document, [starting here](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span></span>

<span data-ttu-id="34c1a-115">Wymagania Wstępne: NSG grupy zasobów, sieciami wirtualnymi, przy użyciu protokołu SSH ruchu przychodzącego, podsieci.</span><span class="sxs-lookup"><span data-stu-id="34c1a-115">Pre-requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span> <span data-ttu-id="34c1a-116">Przykładami należy zastąpić własnymi ustawieniami.</span><span class="sxs-lookup"><span data-stu-id="34c1a-116">Replace any examples with your own settings.</span></span>

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="34c1a-117">Wdrażanie hello maszyny Wirtualnej do hello infrastruktury sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="34c1a-117">Deploy hello VM into hello virtual network infrastructure</span></span>

```azurecli
azure vm create myVM \
    -g myResourceGroup \
    -l eastus \
    -y linux \
    -Q Debian \
    -o mystorageaccount \
    -u myAdminUser \
    -M ~/.ssh/id_rsa.pub \
    -n myVM \
    -F myVNet \
    -j mySubnet \
    -N myVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="34c1a-118">Szczegółowy przewodnik</span><span class="sxs-lookup"><span data-stu-id="34c1a-118">Detailed walkthrough</span></span>

<span data-ttu-id="34c1a-119">Zasoby platformy Azure, takich jak hello sieci wirtualnych i grup zabezpieczeń sieci musi być statyczny i tam długo zasoby, które rzadko są wdrożone.</span><span class="sxs-lookup"><span data-stu-id="34c1a-119">Azure assets like hello VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="34c1a-120">Po wdrożeniu sieci wirtualnej można użyć ponownie przez nowych wdrożeń bez żadnych infrastruktury toohello niekorzystny wpływ.</span><span class="sxs-lookup"><span data-stu-id="34c1a-120">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="34c1a-121">Traktować jako przełącznik sieciowy sprzętu tradycyjnych sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="34c1a-121">Think about a VNet as being a traditional hardware network switch.</span></span> <span data-ttu-id="34c1a-122">Nie trzeba tooconfigure nowego sprzętu przełącznik z każdym wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="34c1a-122">You would not need tooconfigure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="34c1a-123">Z poprawnie skonfigurowana sieć wirtualną możesz kontynuować toodeploy nowych serwerów do tej sieci wirtualnej samodzielnego kilka, zmian wymaganych przez czas życia hello hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="34c1a-123">With a correctly configured VNet, you can continue toodeploy new servers into that VNet over and over with few, if any, changes required over hello life of hello VNet.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="34c1a-124">Utwórz grupę zasobów hello</span><span class="sxs-lookup"><span data-stu-id="34c1a-124">Create hello resource group</span></span>

<span data-ttu-id="34c1a-125">Najpierw utwórz tooorganize grupy zasobów wszystko, czego możesz utworzyć w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="34c1a-125">First, create a resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="34c1a-126">Aby uzyskać więcej informacji na temat grup zasobów, zobacz [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="34c1a-126">For more information about resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-hello-vnet"></a><span data-ttu-id="34c1a-127">Utwórz hello sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="34c1a-127">Create hello VNet</span></span>

<span data-ttu-id="34c1a-128">Witaj pierwszym krokiem jest toobuild maszyn wirtualnych do hello toolaunch sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="34c1a-128">hello first step is toobuild a VNet toolaunch hello VMs into.</span></span> <span data-ttu-id="34c1a-129">Witaj sieć wirtualna zawiera jedną podsieć w ramach tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="34c1a-129">hello VNet contains one subnet for this walkthrough.</span></span> <span data-ttu-id="34c1a-130">Aby uzyskać więcej informacji o sieci wirtualnych platformy Azure, zobacz [utworzyć sieć wirtualną przy użyciu hello wiersza polecenia platformy Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="34c1a-130">For more information on Azure VNets, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span></span>

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="34c1a-131">Utwórz grupę zabezpieczeń sieci hello</span><span class="sxs-lookup"><span data-stu-id="34c1a-131">Create hello network security group</span></span>

<span data-ttu-id="34c1a-132">podsieci Hello jest wbudowana za istniejącej grupy zabezpieczeń sieci tak kompilacji hello sieciowej grupy zabezpieczeń przed hello podsieci.</span><span class="sxs-lookup"><span data-stu-id="34c1a-132">hello subnet is built behind an existing network security group so build hello network security group before hello subnet.</span></span> <span data-ttu-id="34c1a-133">Grupy zabezpieczeń sieci platformy Azure są równoważne tooa zapory na powitania warstwy sieci.</span><span class="sxs-lookup"><span data-stu-id="34c1a-133">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="34c1a-134">Aby uzyskać więcej informacji dotyczących grup zabezpieczeń sieci platformy Azure, zobacz [jak grupy zabezpieczeń sieci toocreate w hello wiersza polecenia platformy Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="34c1a-134">For more information on Azure network security groups, see [How toocreate network security groups in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span></span>

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="34c1a-135">Dodaj regułę Zezwalaj SSH dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="34c1a-135">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="34c1a-136">Witaj maszyna wirtualna musi mieć dostęp z hello internet, regułę zezwalającą na toobe ruch przychodzący port 22 przekazywane hello sieci tooport 22 na powitania maszyny Wirtualnej jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="34c1a-136">hello VM needs access from hello internet so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range 22 \
    --destination-address-prefix 10.10.0.0/24 \
    --destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a><span data-ttu-id="34c1a-137">Dodaj toohello podsieci sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="34c1a-137">Add a subnet toohello VNet</span></span>

<span data-ttu-id="34c1a-138">Maszyny wirtualne w ramach hello sieci wirtualnej muszą znajdować się w podsieci.</span><span class="sxs-lookup"><span data-stu-id="34c1a-138">VMs within hello VNet must be located in a subnet.</span></span> <span data-ttu-id="34c1a-139">Każda sieć wirtualna może mieć wiele podsieci.</span><span class="sxs-lookup"><span data-stu-id="34c1a-139">Each VNet can have multiple subnets.</span></span> <span data-ttu-id="34c1a-140">Utwórz podsieć hello i skojarz z hello sieciowej grupy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="34c1a-140">Create hello subnet and associate with hello network security group.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

<span data-ttu-id="34c1a-141">Hello podsieci jest teraz dodawane wewnątrz hello sieci wirtualnej i skojarzonych z hello sieciowej grupy zabezpieczeń i reguły.</span><span class="sxs-lookup"><span data-stu-id="34c1a-141">hello Subnet is now added inside hello VNet and associated with hello network security group and rule.</span></span>


## <a name="add-a-vnic-toohello-subnet"></a><span data-ttu-id="34c1a-142">Dodaj podsieć toohello VNic</span><span class="sxs-lookup"><span data-stu-id="34c1a-142">Add a VNic toohello subnet</span></span>

<span data-ttu-id="34c1a-143">Wirtualne karty sieciowe (VNics) są ważne, ponieważ późniejszego łącząc je toodifferent maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="34c1a-143">Virtual network cards (VNics) are important as you can reuse them by connecting them toodifferent VMs.</span></span> <span data-ttu-id="34c1a-144">Takie podejście zapewnia hello VNic jako zasób statycznych hello maszyny wirtualne mogą być tymczasowe.</span><span class="sxs-lookup"><span data-stu-id="34c1a-144">This approach keeps hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="34c1a-145">Utwórz VNic i skojarzyć go z podsiecią hello utworzony w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="34c1a-145">Create a VNic and associate it with hello subnet created in hello previous step.</span></span>

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="34c1a-146">Wdrażanie hello maszyny Wirtualnej do hello sieci wirtualnej i grupy NSG</span><span class="sxs-lookup"><span data-stu-id="34c1a-146">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="34c1a-147">Istnieje już sieć wirtualną i podsieci w tej sieci wirtualnej i sieciową grupę zabezpieczeń, stanowiąc podsieci hello tooprotect blokuje cały ruch przychodzący z wyjątkiem port 22 dla protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="34c1a-147">You now have a VNet and subnet inside that VNet, and a network security group acting tooprotect hello subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="34c1a-148">Teraz można wdrożyć Hello maszyny Wirtualnej w tym istniejącej infrastruktury sieci.</span><span class="sxs-lookup"><span data-stu-id="34c1a-148">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="34c1a-149">Przy użyciu interfejsu wiersza polecenia Azure hello i hello `azure vm create` polecenia hello maszyny Wirtualnej systemu Linux jest wdrożony toohello istniejącej grupy zasobów platformy Azure, sieci wirtualnej, podsieci i VNic.</span><span class="sxs-lookup"><span data-stu-id="34c1a-149">Using hello Azure CLI, and hello `azure vm create` command, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span> <span data-ttu-id="34c1a-150">Aby uzyskać więcej informacji na temat używania hello CLI toodeploy pełną maszyny Wirtualnej, zobacz [tworzyć kompletne środowisko systemu Linux przy użyciu interfejsu wiersza polecenia Azure hello](create-cli-complete.md)</span><span class="sxs-lookup"><span data-stu-id="34c1a-150">For more information on using hello CLI toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md)</span></span>

```azurecli
azure vm create myVM \
    --resource-group myResourceGroup \
    --location eastus \
    --os-type linux \
    --image-urn Debian \
    --storage-account-name mystorageaccount \
    --admin-username myAdminUser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --vnet-name myVNet \
    --vnet-subnet-name mySubnet \
    --nic-name myVNic
```

<span data-ttu-id="34c1a-151">Za pomocą hello interfejsu wiersza polecenia flagi toocall limit istniejących zasobów, poinstruuj hello Azure toodeploy VM wewnątrz hello istniejącej sieci.</span><span class="sxs-lookup"><span data-stu-id="34c1a-151">By using hello CLI flags toocall out existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="34c1a-152">Po wdrożeniu sieci wirtualnej i podsieci, możesz je zostawić jako statyczne ani stałe zasoby w Twoim regionie Azure.</span><span class="sxs-lookup"><span data-stu-id="34c1a-152">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="34c1a-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="34c1a-153">Next steps</span></span>

* [<span data-ttu-id="34c1a-154">Użyj toocreate szablonu usługi Azure Resource Manager określonego wdrożenia</span><span class="sxs-lookup"><span data-stu-id="34c1a-154">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="34c1a-155">Tworzenie niestandardowego środowiska dla maszyny wirtualnej z systemem Linux poprzez bezpośrednie użycie poleceń interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="34c1a-155">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="34c1a-156">Utwórz Maszynę wirtualną systemu Linux na platformie Azure za pomocą szablonów</span><span class="sxs-lookup"><span data-stu-id="34c1a-156">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
