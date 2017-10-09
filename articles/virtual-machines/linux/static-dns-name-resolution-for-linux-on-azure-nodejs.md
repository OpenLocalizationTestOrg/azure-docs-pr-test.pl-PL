---
title: "aaaUsing wewnętrzny serwer DNS dla maszyny Wirtualnej do rozpoznawania nazw na platformie Azure | Dokumentacja firmy Microsoft"
description: "Przy użyciu wewnętrznego serwera DNS do rozpoznawania nazw maszyny Wirtualnej na platformie Azure."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/05/2016
ms.author: v-livech
ms.openlocfilehash: 94fd6577aa51ce5db4dc26649b415ddeeb410eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="54144-103">Przy użyciu wewnętrznego serwera DNS do rozpoznawania nazw maszyny Wirtualnej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="54144-103">Using internal DNS for VM name resolution on Azure</span></span>

<span data-ttu-id="54144-104">W tym artykule przedstawiono sposób tooset statycznych wewnętrzny serwer DNS nazwy dla maszyn wirtualnych systemu Linux przy użyciu karty wirtualnej karty Sieciowej (VNic) i nazwy etykiety DNS.</span><span class="sxs-lookup"><span data-stu-id="54144-104">This article shows how tooset static internal DNS names for Linux VMs using Virtual NIC cards (VNic) and DNS label names.</span></span> <span data-ttu-id="54144-105">Statyczne nazwy DNS są używane dla usług trwałych infrastruktury, takich jak serwer kompilacji Wpięć, który służy do tego dokumentu lub serwer Git.</span><span class="sxs-lookup"><span data-stu-id="54144-105">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="54144-106">wymagania dotyczące Hello są:</span><span class="sxs-lookup"><span data-stu-id="54144-106">hello requirements are:</span></span>

* [<span data-ttu-id="54144-107">Konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="54144-107">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="54144-108">Pliki kluczy publicznych i prywatnych SSH</span><span class="sxs-lookup"><span data-stu-id="54144-108">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="54144-109">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="54144-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="54144-110">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="54144-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="54144-111">[Azure CLI 1.0](#quick-commands) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="54144-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="54144-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="54144-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="54144-113">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="54144-113">Quick commands</span></span>

<span data-ttu-id="54144-114">Jeśli potrzebujesz tooquickly hello zadania, powitania po sekcji Szczegóły poleceń hello potrzebne.</span><span class="sxs-lookup"><span data-stu-id="54144-114">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="54144-115">Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć hello pozostałej części dokumentu hello [uruchamiania tutaj](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="54144-115">More detailed information and context for each step can be found hello rest of hello document, [starting here](#detailed-walkthrough).</span></span>  

<span data-ttu-id="54144-116">Wymagania Wstępne: NSG grupy zasobów, sieciami wirtualnymi, przy użyciu protokołu SSH ruchu przychodzącego, podsieci.</span><span class="sxs-lookup"><span data-stu-id="54144-116">Pre-Requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span>

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a><span data-ttu-id="54144-117">Utworzyć VNic statyczne wewnętrzne nazwy DNS</span><span class="sxs-lookup"><span data-stu-id="54144-117">Create a VNic with a static internal DNS name</span></span>

<span data-ttu-id="54144-118">Witaj `-r` Flaga interfejsu wiersza polecenia jest ustawienie hello DNS etykiety, który zapewnia hello statycznej nazwy DNS dla hello VNic.</span><span class="sxs-lookup"><span data-stu-id="54144-118">hello `-r` cli flag is for setting hello DNS label, which provides hello static DNS name for hello VNic.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-hello-vm-into-hello-vnet-nsg-and-connect-hello-vnic"></a><span data-ttu-id="54144-119">Wdrażanie hello maszyny Wirtualnej do hello sieci wirtualnej, NSG i połącz hello VNic</span><span class="sxs-lookup"><span data-stu-id="54144-119">Deploy hello VM into hello VNet, NSG and, connect hello VNic</span></span>

<span data-ttu-id="54144-120">Witaj `-N` łączy hello VNic toohello nowej maszyny Wirtualnej podczas hello tooAzure wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="54144-120">hello `-N` connects hello VNic toohello new VM during hello deployment tooAzure.</span></span>

```azurecli
azure vm create jenkins \
-g myResourceGroup \
-l westus \
-y linux \
-Q Debian \
-o myStorageAcct \
-u myAdminUser \
-M ~/.ssh/id_rsa.pub \
-F myVNet \
-j mySubnet \
-N jenkinsVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="54144-121">Szczegółowy przewodnik</span><span class="sxs-lookup"><span data-stu-id="54144-121">Detailed walkthrough</span></span>

<span data-ttu-id="54144-122">Pełne ciągłej integracji i ciągłe wdrażanie (CiCd) infrastruktury na platformie Azure wymaga niektórych toobe statyczne lub długotrwałe serwery.</span><span class="sxs-lookup"><span data-stu-id="54144-122">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers toobe static or long-lived servers.</span></span>  <span data-ttu-id="54144-123">Zaleca się, że Azure zasoby, takie jak hello sieci wirtualnych (sieci wirtualne) i grupy zabezpieczeń sieci (NSG), musi być statyczny i tam długo zasoby, które rzadko są wdrożone.</span><span class="sxs-lookup"><span data-stu-id="54144-123">It is recommended that Azure assets like hello Virtual Networks (VNets) and Network Security Groups (NSGs), should be static and long lived resources that are rarely deployed.</span></span>  <span data-ttu-id="54144-124">Po wdrożeniu sieci wirtualnej można użyć ponownie przez nowych wdrożeń bez żadnych infrastruktury toohello niekorzystny wpływ.</span><span class="sxs-lookup"><span data-stu-id="54144-124">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span>  <span data-ttu-id="54144-125">Dodawanie sieci statycznych toothis Git repozytorium serwera i serwera automatyzacji Wpięć zapewnia CiCd tooyour środowisk deweloperskich lub testowania.</span><span class="sxs-lookup"><span data-stu-id="54144-125">Adding toothis static network a Git repository server and a Jenkins automation server delivers CiCd tooyour development or test environments.</span></span>  

<span data-ttu-id="54144-126">Wewnętrzny nazw DNS są tylko rozpoznawany w sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="54144-126">Internal DNS names are only resolvable inside an Azure virtual network.</span></span>  <span data-ttu-id="54144-127">Ponieważ nazwy DNS hello są wewnętrzne, nie są one rozpoznawalną toohello poza internet, zapewniając dodatkowe zabezpieczenia toohello infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="54144-127">Because hello DNS names are internal, they are not resolvable toohello outside internet, providing additional security toohello infrastructure.</span></span>

<span data-ttu-id="54144-128">_Przykładami Zamień własne nazwy._</span><span class="sxs-lookup"><span data-stu-id="54144-128">_Replace any examples with your own naming._</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="54144-129">Utwórz grupę zasobów hello</span><span class="sxs-lookup"><span data-stu-id="54144-129">Create hello Resource group</span></span>

<span data-ttu-id="54144-130">Grupa zasobów jest wymagane tooorganize wszystko, co mamy utworzyć w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="54144-130">A Resource Group is needed tooorganize everything we create in this walkthrough.</span></span>  <span data-ttu-id="54144-131">Aby uzyskać więcej informacji na temat grup zasobów platformy Azure, zobacz [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="54144-131">For more information on Azure Resource Groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-hello-vnet"></a><span data-ttu-id="54144-132">Utwórz hello sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="54144-132">Create hello VNet</span></span>

<span data-ttu-id="54144-133">Witaj pierwszym krokiem jest toobuild maszyn wirtualnych do hello toolaunch sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="54144-133">hello first step is toobuild a VNet toolaunch hello VMs into.</span></span>  <span data-ttu-id="54144-134">Witaj sieć wirtualna zawiera jedną podsieć w ramach tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="54144-134">hello VNet contains one subnet for this walkthrough.</span></span>  <span data-ttu-id="54144-135">Aby uzyskać więcej informacji o sieci wirtualnych platformy Azure, zobacz [utworzyć sieć wirtualną przy użyciu hello wiersza polecenia platformy Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="54144-135">For more information on Azure VNets, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-hello-nsg"></a><span data-ttu-id="54144-136">Utwórz hello NSG</span><span class="sxs-lookup"><span data-stu-id="54144-136">Create hello NSG</span></span>

<span data-ttu-id="54144-137">Witaj podsieci jest oparty za istniejącą sieciową grupę zabezpieczeń, dlatego budujemy hello NSG przed hello podsieci.</span><span class="sxs-lookup"><span data-stu-id="54144-137">hello Subnet is built behind an existing Network Security Group so we build hello NSG before hello Subnet.</span></span>  <span data-ttu-id="54144-138">Azure grup NSG są równoważne tooa zapory na powitania warstwy sieci.</span><span class="sxs-lookup"><span data-stu-id="54144-138">Azure NSGs are equivalent tooa firewall at hello network layer.</span></span>  <span data-ttu-id="54144-139">Aby uzyskać więcej informacji dotyczących grup NSG Azure, zobacz [jak grupy NSG toocreate w hello wiersza polecenia platformy Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="54144-139">For more information on Azure NSGs, see [How toocreate NSGs in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="54144-140">Dodaj regułę Zezwalaj SSH dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="54144-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="54144-141">Witaj maszyny Wirtualnej systemu Linux wymaga dostępu z hello jest wymagana przez internet, regułę zezwalającą na toobe 22 ruch przychodzący port przekazywane hello sieci tooport 22 na powitania maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="54144-141">hello Linux VM needs access from hello internet so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello Linux VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
--resource-group myResourceGroup \
--nsg-name myNSG \
--access Allow \
--protocol Tcp \
--direction Inbound \
--priority 100 \
--source-address-prefix * \
--source-port-range * \
--destination-address-prefix 10.10.0.0/24 \
--destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a><span data-ttu-id="54144-142">Dodaj toohello podsieci sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="54144-142">Add a subnet toohello VNet</span></span>

<span data-ttu-id="54144-143">Maszyny wirtualne w ramach hello sieci wirtualnej muszą znajdować się w podsieci.</span><span class="sxs-lookup"><span data-stu-id="54144-143">VMs within hello VNet must be located in a subnet.</span></span>  <span data-ttu-id="54144-144">Każda sieć wirtualna może mieć wiele podsieci.</span><span class="sxs-lookup"><span data-stu-id="54144-144">Each VNet can have multiple subnets.</span></span>  <span data-ttu-id="54144-145">Utwórz podsieć hello i podsieć hello skojarzona z hello tooadd NSG podsieci toohello zapory.</span><span class="sxs-lookup"><span data-stu-id="54144-145">Create hello subnet and associate hello subnet with hello NSG tooadd a firewall toohello subnet.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

<span data-ttu-id="54144-146">Hello podsieci jest teraz dodawane wewnątrz hello sieci wirtualnej i skojarzonych z hello NSG i reguły NSG hello.</span><span class="sxs-lookup"><span data-stu-id="54144-146">hello Subnet is now added inside hello VNet and associated with hello NSG and hello NSG rule.</span></span>

## <a name="creating-static-dns-names"></a><span data-ttu-id="54144-147">Tworzenie statycznej nazwy DNS</span><span class="sxs-lookup"><span data-stu-id="54144-147">Creating static DNS names</span></span>

<span data-ttu-id="54144-148">Azure jest bardzo elastyczny, ale toouse nazwy DNS dla rozpoznawania nazw maszyn wirtualnych, należy je jako wirtualnej sieci karty (VNics) przy użyciu systemu DNS etykietowania toocreate.</span><span class="sxs-lookup"><span data-stu-id="54144-148">Azure is very flexible, but toouse DNS names for VMs name resolution, you need toocreate them as Virtual network cards (VNics) using DNS labeling.</span></span>  <span data-ttu-id="54144-149">VNics są ważne, ponieważ użytkownik może korzystać z nich łącząc je toodifferent maszyn wirtualnych, które hello VNic jako zasób statycznych hello maszyny wirtualne mogą być tymczasowe.</span><span class="sxs-lookup"><span data-stu-id="54144-149">VNics are important as you can reuse them by connecting them toodifferent VMs, which keeps hello VNic as a static resource while hello VMs can be temporary.</span></span>  <span data-ttu-id="54144-150">Przy użyciu systemu DNS etykietowania na powitania VNic, możemy rozpoznawania nazw proste stanie tooenable z innych maszyn wirtualnych w hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="54144-150">By using DNS labeling on hello VNic, we are able tooenable simple name resolution from other VMs in hello VNet.</span></span>  <span data-ttu-id="54144-151">Przy użyciu nazwy rozpoznawalną umożliwia inny serwer automatyzacji hello tooaccess maszyn wirtualnych na podstawie nazwy DNS hello `Jenkins` lub na serwerze Git hello `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="54144-151">Using resolvable names enables other VMs tooaccess hello automation server by hello DNS name `Jenkins` or hello Git server as `gitrepo`.</span></span>  <span data-ttu-id="54144-152">Utwórz VNic i powiązać ją z hello utworzone w poprzednim kroku hello podsieci.</span><span class="sxs-lookup"><span data-stu-id="54144-152">Create a VNic and associate it with hello Subnet created in hello previous step.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="54144-153">Wdrażanie hello maszyny Wirtualnej do hello sieci wirtualnej i grupy NSG</span><span class="sxs-lookup"><span data-stu-id="54144-153">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="54144-154">Mamy teraz sieci wirtualnej, podsieci w tej sieci wirtualnej, a grupa NSG, działając jako tooprotect zapory naszych podsieci blokuje cały ruch przychodzący z wyjątkiem port 22 SSH.</span><span class="sxs-lookup"><span data-stu-id="54144-154">We now have a VNet, a subnet inside that VNet, and an NSG acting as a firewall tooprotect our subnet by blocking all inbound traffic except port 22 for SSH.</span></span>  <span data-ttu-id="54144-155">Teraz można wdrożyć Hello maszyny Wirtualnej w tym istniejącej infrastruktury sieci.</span><span class="sxs-lookup"><span data-stu-id="54144-155">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="54144-156">Przy użyciu interfejsu wiersza polecenia Azure hello i hello `azure vm create` polecenia hello maszyny Wirtualnej systemu Linux jest wdrożony toohello istniejącej grupy zasobów platformy Azure, sieci wirtualnej, podsieci i VNic.</span><span class="sxs-lookup"><span data-stu-id="54144-156">Using hello Azure CLI, and hello `azure vm create` command, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>  <span data-ttu-id="54144-157">Aby uzyskać więcej informacji na temat używania hello CLI toodeploy pełną maszyny Wirtualnej, zobacz [tworzyć kompletne środowisko systemu Linux przy użyciu interfejsu wiersza polecenia Azure hello](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="54144-157">For more information on using hello CLI toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure vm create jenkins \
--resource-group myResourceGroup myVM \
--location westus \
--os-type linux \
--image-urn Debian \
--storage-account-name mystorageaccount \
--admin-username myAdminUser \
--ssh-publickey-file ~/.ssh/id_rsa.pub \
--vnet-name myVNet \
--vnet-subnet-name mySubnet \
--nic-name jenkinsVNic
```

<span data-ttu-id="54144-158">Za pomocą hello interfejsu wiersza polecenia flagi toocall limit istniejących zasobów, firma Microsoft poinstruować hello Azure toodeploy VM wewnątrz hello istniejącej sieci.</span><span class="sxs-lookup"><span data-stu-id="54144-158">By using hello CLI flags toocall out existing resources, we instruct Azure toodeploy hello VM inside hello existing network.</span></span>  <span data-ttu-id="54144-159">tooreiterate, po wdrożeniu sieci wirtualnej i podsieci, ich może pozostać statyczne ani stałe zasobów w Twoim regionie Azure.</span><span class="sxs-lookup"><span data-stu-id="54144-159">tooreiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="54144-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="54144-160">Next steps</span></span>
* [<span data-ttu-id="54144-161">Tworzenie niestandardowego środowiska dla maszyny wirtualnej z systemem Linux poprzez bezpośrednie użycie poleceń interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="54144-161">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="54144-162">Utwórz Maszynę wirtualną systemu Linux na platformie Azure za pomocą szablonów</span><span class="sxs-lookup"><span data-stu-id="54144-162">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
