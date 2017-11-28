---
title: "Wdrażanie maszyn wirtualnych systemu Linux w istniejącej sieci z interfejsu wiersza polecenia platformy Azure w wersji 1.0 | Dokumentacja firmy Microsoft"
description: "Jak wdrożyć Maszynę wirtualną systemu Linux w ramach istniejącej sieci wirtualnej przy użyciu 1.0 interfejsu wiersza polecenia platformy Azure"
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
ms.openlocfilehash: 767a3f7cadba6b1e71e5a8f5995a9db090e419dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-cli-10"></a><span data-ttu-id="a7af6-103">Jak wdrożyć maszyny wirtualnej systemu Linux w istniejącej sieci wirtualnej platformy Azure z interfejsu wiersza polecenia platformy Azure w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="a7af6-103">How to deploy a Linux virtual machine into an existing Azure Virtual Network with the Azure CLI 1.0</span></span>

<span data-ttu-id="a7af6-104">W tym artykule przedstawiono sposób użycia interfejsu wiersza polecenia platformy Azure w wersji 1.0, aby wdrożyć maszynę wirtualną (VM) do istniejącej sieci wirtualnej (VNet).</span><span class="sxs-lookup"><span data-stu-id="a7af6-104">This article shows you how to use Azure CLI 1.0 to deploy a virtual machine (VM) into an existing Virtual Network (VNet).</span></span> <span data-ttu-id="a7af6-105">Wymagania są następujące:</span><span class="sxs-lookup"><span data-stu-id="a7af6-105">The requirements are:</span></span>

- [<span data-ttu-id="a7af6-106">Konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a7af6-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="a7af6-107">Pliki kluczy publicznych i prywatnych SSH</span><span class="sxs-lookup"><span data-stu-id="a7af6-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="a7af6-108">Wersje interfejsu wiersza polecenia umożliwiające wykonanie zadania</span><span class="sxs-lookup"><span data-stu-id="a7af6-108">CLI versions to complete the task</span></span>
<span data-ttu-id="a7af6-109">Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="a7af6-109">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="a7af6-110">[Azure CLI 1.0](#quick-commands) — nasze interfejsu wiersza polecenia dla klasycznego i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="a7af6-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="a7af6-111">[Interfejs wiersza polecenia platformy Azure w wersji 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) — nasz interfejs wiersza polecenia nowej generacji dla modelu wdrażania na potrzeby zarządzania zasobami</span><span class="sxs-lookup"><span data-stu-id="a7af6-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="a7af6-112">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="a7af6-112">Quick Commands</span></span>

<span data-ttu-id="a7af6-113">Jeśli chcesz szybko wykonywać zadania poniższej sekcji Szczegóły poleceń potrzebne.</span><span class="sxs-lookup"><span data-stu-id="a7af6-113">If you need to quickly accomplish the task, the following section details the commands needed.</span></span> <span data-ttu-id="a7af6-114">Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć pozostałej części dokumentu, [uruchamiania tutaj](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="a7af6-114">More detailed information and context for each step can be found the rest of the document, [starting here](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span></span>

<span data-ttu-id="a7af6-115">Wymagania Wstępne: NSG grupy zasobów, sieciami wirtualnymi, przy użyciu protokołu SSH ruchu przychodzącego, podsieci.</span><span class="sxs-lookup"><span data-stu-id="a7af6-115">Pre-requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span> <span data-ttu-id="a7af6-116">Przykładami należy zastąpić własnymi ustawieniami.</span><span class="sxs-lookup"><span data-stu-id="a7af6-116">Replace any examples with your own settings.</span></span>

### <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="a7af6-117">Wdróż maszynę Wirtualną do infrastruktury sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a7af6-117">Deploy the VM into the virtual network infrastructure</span></span>

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

## <a name="detailed-walkthrough"></a><span data-ttu-id="a7af6-118">Szczegółowy przewodnik</span><span class="sxs-lookup"><span data-stu-id="a7af6-118">Detailed walkthrough</span></span>

<span data-ttu-id="a7af6-119">Zasoby platformy Azure, takich jak sieci wirtualnych i grup zabezpieczeń sieci musi być statyczny i tam długo zasoby, które rzadko są wdrożone.</span><span class="sxs-lookup"><span data-stu-id="a7af6-119">Azure assets like the VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="a7af6-120">Po wdrożeniu sieci wirtualnej można użyć ponownie przez nowych wdrożeń bez żadnych niekorzystny wpływ infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="a7af6-120">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="a7af6-121">Traktować jako przełącznik sieciowy sprzętu tradycyjnych sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a7af6-121">Think about a VNet as being a traditional hardware network switch.</span></span> <span data-ttu-id="a7af6-122">Nie musisz skonfigurować nowy przełącznik sprzętu z każdym wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="a7af6-122">You would not need to configure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="a7af6-123">Z poprawnie skonfigurowana sieć wirtualną możesz kontynuować wdrażanie nowych serwerów w tej sieci wirtualnej samodzielnego z kilku ewentualne zmiany wymagane w całej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a7af6-123">With a correctly configured VNet, you can continue to deploy new servers into that VNet over and over with few, if any, changes required over the life of the VNet.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="a7af6-124">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="a7af6-124">Create the resource group</span></span>

<span data-ttu-id="a7af6-125">Najpierw utwórz grupę zasobów do organizowania wszystko, czego możesz utworzyć w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="a7af6-125">First, create a resource group to organize everything you create in this walkthrough.</span></span> <span data-ttu-id="a7af6-126">Aby uzyskać więcej informacji na temat grup zasobów, zobacz [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a7af6-126">For more information about resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-the-vnet"></a><span data-ttu-id="a7af6-127">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a7af6-127">Create the VNet</span></span>

<span data-ttu-id="a7af6-128">Pierwszym krokiem jest kompilacji do uruchamiania maszyn wirtualnych do sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a7af6-128">The first step is to build a VNet to launch the VMs into.</span></span> <span data-ttu-id="a7af6-129">Sieć wirtualna zawiera jedną podsieć w ramach tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="a7af6-129">The VNet contains one subnet for this walkthrough.</span></span> <span data-ttu-id="a7af6-130">Aby uzyskać więcej informacji o sieci wirtualnych platformy Azure, zobacz [utworzyć sieć wirtualną przy użyciu wiersza polecenia platformy Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="a7af6-130">For more information on Azure VNets, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span></span>

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-the-network-security-group"></a><span data-ttu-id="a7af6-131">Utwórz grupę zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="a7af6-131">Create the network security group</span></span>

<span data-ttu-id="a7af6-132">Podsieć jest wbudowana za istniejącej sieci grupy zabezpieczeń tak Tworzenie grupy zabezpieczeń sieci przed podsieci.</span><span class="sxs-lookup"><span data-stu-id="a7af6-132">The subnet is built behind an existing network security group so build the network security group before the subnet.</span></span> <span data-ttu-id="a7af6-133">Grupy zabezpieczeń sieci platformy Azure są równoważne zapory w warstwie sieci.</span><span class="sxs-lookup"><span data-stu-id="a7af6-133">Azure network security groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="a7af6-134">Aby uzyskać więcej informacji dotyczących grup zabezpieczeń sieci platformy Azure, zobacz [sposobu tworzenia grup zabezpieczeń sieci na platformie Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="a7af6-134">For more information on Azure network security groups, see [How to create network security groups in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span></span>

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="a7af6-135">Dodaj regułę Zezwalaj SSH dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="a7af6-135">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="a7af6-136">Maszyna wirtualna wymaga dostępu z Internetu, więc regułę zezwalającą na ruch przychodzący port 22 mają być przekazywane za pośrednictwem sieci do portu 22 na maszynie Wirtualnej nie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="a7af6-136">The VM needs access from the internet so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the VM is needed.</span></span>

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

## <a name="add-a-subnet-to-the-vnet"></a><span data-ttu-id="a7af6-137">Dodaj podsieć do sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a7af6-137">Add a subnet to the VNet</span></span>

<span data-ttu-id="a7af6-138">Maszyny wirtualne w ramach sieci wirtualnej muszą znajdować się w podsieci.</span><span class="sxs-lookup"><span data-stu-id="a7af6-138">VMs within the VNet must be located in a subnet.</span></span> <span data-ttu-id="a7af6-139">Każda sieć wirtualna może mieć wiele podsieci.</span><span class="sxs-lookup"><span data-stu-id="a7af6-139">Each VNet can have multiple subnets.</span></span> <span data-ttu-id="a7af6-140">Utwórz podsieć i skojarzyć z sieciową grupą zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="a7af6-140">Create the subnet and associate with the network security group.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

<span data-ttu-id="a7af6-141">Podsieć jest teraz dodany wewnątrz sieci wirtualnej i skojarzonych z grupy zabezpieczeń sieci i reguły.</span><span class="sxs-lookup"><span data-stu-id="a7af6-141">The Subnet is now added inside the VNet and associated with the network security group and rule.</span></span>


## <a name="add-a-vnic-to-the-subnet"></a><span data-ttu-id="a7af6-142">Dodaj VNic do podsieci</span><span class="sxs-lookup"><span data-stu-id="a7af6-142">Add a VNic to the subnet</span></span>

<span data-ttu-id="a7af6-143">Wirtualne karty sieciowe (VNics) są istotne, ponieważ użytkownik może korzystać z nich łącząc je do różnych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="a7af6-143">Virtual network cards (VNics) are important as you can reuse them by connecting them to different VMs.</span></span> <span data-ttu-id="a7af6-144">Takie podejście zapewnia VNic jako zasób statycznych maszyn wirtualnych mogą być tymczasowe.</span><span class="sxs-lookup"><span data-stu-id="a7af6-144">This approach keeps the VNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="a7af6-145">Utwórz VNic i skojarzyć go z podsiecią utworzony w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="a7af6-145">Create a VNic and associate it with the subnet created in the previous step.</span></span>

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a><span data-ttu-id="a7af6-146">Wdróż maszynę Wirtualną do sieci wirtualnej i grupy NSG</span><span class="sxs-lookup"><span data-stu-id="a7af6-146">Deploy the VM into the VNet and NSG</span></span>

<span data-ttu-id="a7af6-147">Istnieje już sieć wirtualną i podsieci w tej sieci wirtualnej, a grupa zabezpieczeń sieci w celu ochrony podsieci blokuje cały ruch przychodzący z wyjątkiem port 22 dla protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="a7af6-147">You now have a VNet and subnet inside that VNet, and a network security group acting to protect the subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="a7af6-148">Teraz można wdrożyć maszyny Wirtualnej w tym istniejącej infrastruktury sieci.</span><span class="sxs-lookup"><span data-stu-id="a7af6-148">The VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="a7af6-149">Przy użyciu interfejsu wiersza polecenia Azure i `azure vm create` polecenia do istniejącej grupy zasobów platformy Azure, sieci wirtualnej, podsieci i VNic wdrożeniu maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="a7af6-149">Using the Azure CLI, and the `azure vm create` command, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span></span> <span data-ttu-id="a7af6-150">Aby uzyskać więcej informacji na instalację pełną maszyny Wirtualnej za pomocą interfejsu wiersza polecenia, zobacz [tworzyć kompletne środowisko systemu Linux przy użyciu wiersza polecenia platformy Azure](create-cli-complete.md)</span><span class="sxs-lookup"><span data-stu-id="a7af6-150">For more information on using the CLI to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md)</span></span>

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

<span data-ttu-id="a7af6-151">Za pomocą flag interfejsu wiersza polecenia do wyróżnienia istniejących zasobów, można nakazać Azure, aby wdrożyć maszynę Wirtualną w istniejącej sieci.</span><span class="sxs-lookup"><span data-stu-id="a7af6-151">By using the CLI flags to call out existing resources, you instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="a7af6-152">Po wdrożeniu sieci wirtualnej i podsieci, możesz je zostawić jako statyczne ani stałe zasoby w Twoim regionie Azure.</span><span class="sxs-lookup"><span data-stu-id="a7af6-152">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="a7af6-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a7af6-153">Next steps</span></span>

* [<span data-ttu-id="a7af6-154">Tworzenie konkretnego wdrożenia za pomocą szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a7af6-154">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="a7af6-155">Tworzenie niestandardowego środowiska dla maszyny wirtualnej z systemem Linux poprzez bezpośrednie użycie poleceń interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a7af6-155">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="a7af6-156">Utwórz Maszynę wirtualną systemu Linux na platformie Azure za pomocą szablonów</span><span class="sxs-lookup"><span data-stu-id="a7af6-156">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
