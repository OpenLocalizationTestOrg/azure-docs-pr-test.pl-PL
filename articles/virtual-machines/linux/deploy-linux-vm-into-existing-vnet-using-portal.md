---
title: "aaaDeploy maszyn wirtualnych systemu Linux w istniejącej sieci z portalu Azure | Dokumentacja firmy Microsoft"
description: "Wdróż Maszynę wirtualną systemu Linux w istniejącej sieci wirtualnej platformy Azure przy użyciu portalu hello."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 51272b8cdb1dc7f3fe768d2ebbf4ebe0d754cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-portal"></a><span data-ttu-id="f0bd5-103">Jak toodeploy maszyny wirtualnej systemu Linux w istniejącej sieci wirtualnej platformy Azure z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f0bd5-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure portal</span></span>

<span data-ttu-id="f0bd5-104">W tym artykule opisano sposób toodeploy maszynę wirtualną (VM) do istniejącej sieci wirtualnej (VNet).</span><span class="sxs-lookup"><span data-stu-id="f0bd5-104">This article shows you how toodeploy a virtual machine (VM) into an existing virtual network (VNet).</span></span> <span data-ttu-id="f0bd5-105">Azure zasoby, takie jak grupy zabezpieczeń sieci wirtualnych i sieci musi być statyczny i tam długo zasoby, które rzadko są wdrożone.</span><span class="sxs-lookup"><span data-stu-id="f0bd5-105">Azure assets like VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="f0bd5-106">Po wdrożeniu sieci wirtualnej można użyć ponownie przez stałej redeployments bez żadnych infrastruktury toohello niekorzystny wpływ.</span><span class="sxs-lookup"><span data-stu-id="f0bd5-106">Once a VNet has been deployed, it can be reused by constant redeployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="f0bd5-107">Planowanie sieci wirtualnej jako tradycyjną przełącznik sieciowy sprzętu — nie trzeba tooconfigure nowego sprzętu przełącznik z każdym wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="f0bd5-107">Thinking about a VNet as being a traditional hardware network switch - you would not need tooconfigure a brand new hardware switch with each deployment.</span></span>  

<span data-ttu-id="f0bd5-108">Z poprawnie skonfigurowana sieć wirtualną możesz kontynuować toodeploy nowych serwerów do tej sieci wirtualnej samodzielnego kilka, zmian wymaganych przez czas życia hello hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f0bd5-108">With a correctly configured VNet, you can continue toodeploy new servers into that VNet over and over with few, if any, changes required over hello life of hello VNet.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="f0bd5-109">Utwórz grupę zasobów hello</span><span class="sxs-lookup"><span data-stu-id="f0bd5-109">Create hello resource group</span></span>

<span data-ttu-id="f0bd5-110">Najpierw utwórz tooorganize grupy zasobów wszystko, czego możesz utworzyć w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="f0bd5-110">First, create a resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="f0bd5-111">Aby uzyskać więcej informacji na temat grup zasobów platformy Azure, zobacz [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f0bd5-111">For more information about Azure resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-hello-vnet"></a><span data-ttu-id="f0bd5-113">Utwórz hello sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f0bd5-113">Create hello VNet</span></span>

<span data-ttu-id="f0bd5-114">Następnie kompilacji hello toolaunch sieci wirtualnej maszyn wirtualnych do.</span><span class="sxs-lookup"><span data-stu-id="f0bd5-114">Next, build a VNet toolaunch hello VMs into.</span></span> <span data-ttu-id="f0bd5-115">Hello sieć wirtualna zawiera jedną podsieć i jest skojarzona z sieciową grupą zabezpieczeń hello z tą podsiecią w kolejnym kroku.</span><span class="sxs-lookup"><span data-stu-id="f0bd5-115">hello VNet contains one subnet and is associated with hello network security group with this subnet in a later step.</span></span>

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-toohello-subnet"></a><span data-ttu-id="f0bd5-117">Dodaj podsieć toohello VNic</span><span class="sxs-lookup"><span data-stu-id="f0bd5-117">Add a VNic toohello subnet</span></span>

<span data-ttu-id="f0bd5-118">Wirtualne karty sieciowe (VNics) są ważne, jak można je połączyć toodifferent maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f0bd5-118">Virtual network cards (VNics) are important as you can connect them toodifferent VMs.</span></span> <span data-ttu-id="f0bd5-119">Takie podejście zapewnia hello VNic jako zasób statycznych hello maszyny wirtualne mogą być tymczasowe.</span><span class="sxs-lookup"><span data-stu-id="f0bd5-119">This approach keeps hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="f0bd5-120">Utwórz VNic i skojarzyć go z podsiecią hello utworzony w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="f0bd5-120">Create a VNic and associate it with hello subnet created in hello previous step.</span></span>

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-hello-network-security-group"></a><span data-ttu-id="f0bd5-122">Utwórz grupę zabezpieczeń sieci hello</span><span class="sxs-lookup"><span data-stu-id="f0bd5-122">Create hello network security group</span></span>

<span data-ttu-id="f0bd5-123">Grupy zabezpieczeń sieci platformy Azure są równoważne tooa zapory na powitania warstwy sieci.</span><span class="sxs-lookup"><span data-stu-id="f0bd5-123">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="f0bd5-124">Aby uzyskać więcej informacji dotyczących grup zabezpieczeń sieci platformy Azure, zobacz [co to jest grupa zabezpieczeń sieci](../../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="f0bd5-124">For more information on Azure network security groups, see [What is a Network Security Group](../../virtual-network/virtual-networks-nsg.md).</span></span>

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="f0bd5-126">Dodaj regułę Zezwalaj SSH dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="f0bd5-126">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="f0bd5-127">Witaj maszyna wirtualna musi mieć dostęp z hello internet, więc regułę zezwalającą na toobe ruch przychodzący port 22 przekazywane hello sieci tooport 22 na powitania zostanie utworzona maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="f0bd5-127">hello VM needs access from hello internet, so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is created.</span></span>

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-hello-nsg-with-hello-subnet"></a><span data-ttu-id="f0bd5-129">Skojarz hello grupy NSG z podsiecią hello</span><span class="sxs-lookup"><span data-stu-id="f0bd5-129">Associate hello NSG with hello subnet</span></span>

<span data-ttu-id="f0bd5-130">Z hello sieć wirtualną i podsieć hello utworzona należy skojarzyć hello sieciową grupę zabezpieczeń z podsiecią hello.</span><span class="sxs-lookup"><span data-stu-id="f0bd5-130">With hello VNet and hello subnet created, associate hello network security group with hello subnet.</span></span> <span data-ttu-id="f0bd5-131">Może być skojarzony z całej podsieci lub VNic poszczególnych grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="f0bd5-131">Network security groups can be associated with either an entire subnet or an individual VNic.</span></span> <span data-ttu-id="f0bd5-132">Zapora hello filtrowanie ruchu na poziomie podsieci hello wszystkich VNics i hello maszyn wirtualnych w obrębie podsieci hello są chronione przez hello sieciowej grupy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="f0bd5-132">With hello firewall filtering traffic at hello subnet level, all VNics and hello VMs within hello subnet are protected by hello network security group.</span></span> <span data-ttu-id="f0bd5-133">Witaj innej metody jest hello jest grupa zabezpieczeń sieci skojarzonych z tylko jednym kartę VNic i chronienie tylko jednej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f0bd5-133">hello other approach is hello network security group being associated with just a single VNic and protecting just one VM.</span></span>

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="f0bd5-135">Wdrażanie hello maszyny Wirtualnej do hello sieci wirtualnej i grupy NSG</span><span class="sxs-lookup"><span data-stu-id="f0bd5-135">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="f0bd5-136">Przy użyciu hello portalu Azure, hello maszyny Wirtualnej systemu Linux jest wdrożony toohello istniejącej grupy zasobów platformy Azure, sieci wirtualnej, podsieci i VNic.</span><span class="sxs-lookup"><span data-stu-id="f0bd5-136">Using hello Azure portal, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

<span data-ttu-id="f0bd5-138">Za pomocą portalu toochoose hello istniejących zasobów, poinstruuj Azure toodeploy hello wirtualna wewnątrz hello istniejącej sieci.</span><span class="sxs-lookup"><span data-stu-id="f0bd5-138">By using hello portal toochoose existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="f0bd5-139">Po wdrożeniu sieci wirtualnej i podsieci, możesz je zostawić jako statyczne ani stałe zasoby w Twoim regionie Azure.</span><span class="sxs-lookup"><span data-stu-id="f0bd5-139">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="f0bd5-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f0bd5-140">Next steps</span></span>

* [<span data-ttu-id="f0bd5-141">Użyj toocreate szablonu usługi Azure Resource Manager określonego wdrożenia</span><span class="sxs-lookup"><span data-stu-id="f0bd5-141">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="f0bd5-142">Tworzenie niestandardowego środowiska dla maszyny wirtualnej z systemem Linux poprzez bezpośrednie użycie poleceń interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f0bd5-142">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="f0bd5-143">Utwórz Maszynę wirtualną systemu Linux na platformie Azure za pomocą szablonów</span><span class="sxs-lookup"><span data-stu-id="f0bd5-143">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
