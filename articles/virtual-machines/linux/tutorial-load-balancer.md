---
title: aaaHow tooload saldo maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse hello Azure obciążenia toocreate równoważenia aplikacji wysokiej dostępności i bezpieczne w trzech maszyn wirtualnych systemu Linux"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: f01752c3caec3489ee13e63000775769f3236e11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-linux-virtual-machines-in-azure-toocreate-a-highly-available-application"></a><span data-ttu-id="4cb35-103">Jak tooload saldo maszyn wirtualnych systemu Linux w Azure toocreate wysokiej dostępności aplikacji</span><span class="sxs-lookup"><span data-stu-id="4cb35-103">How tooload balance Linux virtual machines in Azure toocreate a highly available application</span></span>
<span data-ttu-id="4cb35-104">Równoważenie obciążenia sieciowego zapewnia wyższy poziom dostępności dzięki rozproszeniu przychodzące żądania między wieloma maszynami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="4cb35-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="4cb35-105">Z tego samouczka dowiesz się o hello różnych składników usługi równoważenia obciążenia Azure hello dystrybucji ruchu, które zapewniają wysoką dostępność.</span><span class="sxs-lookup"><span data-stu-id="4cb35-105">In this tutorial, you learn about hello different components of hello Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="4cb35-106">Omawiane kwestie:</span><span class="sxs-lookup"><span data-stu-id="4cb35-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4cb35-107">Tworzenie usługi równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="4cb35-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="4cb35-108">Utwórz kondycji sondę modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="4cb35-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="4cb35-109">Tworzenie reguły ruchu usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="4cb35-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="4cb35-110">Użyj toocreate init chmury podstawowej aplikacji Node.js</span><span class="sxs-lookup"><span data-stu-id="4cb35-110">Use cloud-init toocreate a basic Node.js app</span></span>
> * <span data-ttu-id="4cb35-111">Tworzenie maszyn wirtualnych i Dołącz tooa modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="4cb35-111">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="4cb35-112">Wyświetl modułu równoważenia obciążenia w akcji</span><span class="sxs-lookup"><span data-stu-id="4cb35-112">View a load balancer in action</span></span>
> * <span data-ttu-id="4cb35-113">Dodawanie i usuwanie maszyny wirtualne z modułem równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="4cb35-113">Add and remove VMs from a load balancer</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4cb35-114">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="4cb35-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="4cb35-115">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="4cb35-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="4cb35-116">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4cb35-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="azure-load-balancer-overview"></a><span data-ttu-id="4cb35-117">Omówienie usługi równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="4cb35-117">Azure load balancer overview</span></span>
<span data-ttu-id="4cb35-118">Moduł równoważenia obciążenia Azure jest równoważenia obciążenia warstwy 4 (TCP, UDP), który zapewnia wysoką dostępność, przekazując przychodzący ruch między maszynami wirtualnymi w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="4cb35-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="4cb35-119">Kondycji sondę modułu równoważenia obciążenia monitoruje danego portu na każdej maszynie Wirtualnej, a tylko dystrybuuje ruch tooan operacyjne maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4cb35-119">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

<span data-ttu-id="4cb35-120">Należy zdefiniować frontonu konfiguracji adresu IP, który zawiera co najmniej jeden publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="4cb35-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="4cb35-121">Ta konfiguracja frontonu IP umożliwia toobe, a aplikacje usługi równoważenia obciążenia dostępny za pośrednictwem hello Internet.</span><span class="sxs-lookup"><span data-stu-id="4cb35-121">This front-end IP configuration allows your load balancer and applications toobe accessible over hello Internet.</span></span> 

<span data-ttu-id="4cb35-122">Maszyny wirtualne połączenie usługi równoważenia obciążenia tooa przy użyciu ich karty interfejsu sieci wirtualnej (NIC).</span><span class="sxs-lookup"><span data-stu-id="4cb35-122">Virtual machines connect tooa load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="4cb35-123">toodistribute toohello ruch maszyn wirtualnych, puli adresów zaplecza zawiera adresy IP hello hello wirtualnych (NIC) toohello podłączonej usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="4cb35-123">toodistribute traffic toohello VMs, a back-end address pool contains hello IP addresses of hello virtual (NICs) connected toohello load balancer.</span></span>

<span data-ttu-id="4cb35-124">toocontrol hello przepływu ruchu, należy zdefiniować reguły modułu równoważenia obciążenia dla określonych portów i protokołów, które mapują tooyour maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="4cb35-124">toocontrol hello flow of traffic, you define load balancer rules for specific ports and protocols that map tooyour VMs.</span></span>

<span data-ttu-id="4cb35-125">Po wykonaniu poprzednich samouczek hello zbyt[utworzyć zestaw skali maszyny wirtualnej](tutorial-create-vmss.md), usługi równoważenia obciążenia został utworzony.</span><span class="sxs-lookup"><span data-stu-id="4cb35-125">If you followed hello previous tutorial too[create a virtual machine scale set](tutorial-create-vmss.md), a load balancer was created for you.</span></span> <span data-ttu-id="4cb35-126">Wszystkie te składniki zostały skonfigurowane dla Ciebie jako część zestawu skalowania hello.</span><span class="sxs-lookup"><span data-stu-id="4cb35-126">All these components were configured for you as part of hello scale set.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="4cb35-127">Tworzenie usługi równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="4cb35-127">Create Azure load balancer</span></span>
<span data-ttu-id="4cb35-128">W tej sekcji Szczegóły, jak można tworzyć i konfigurować poszczególnych składników usługi równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="4cb35-128">This section details how you can create and configure each component of hello load balancer.</span></span> <span data-ttu-id="4cb35-129">Przed utworzeniem przez moduł równoważenia obciążenia, Utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="4cb35-129">Before you can create your load balancer, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="4cb35-130">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupLoadBalancer* w hello *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="4cb35-130">hello following example creates a resource group named *myResourceGroupLoadBalancer* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="4cb35-131">Tworzenie publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="4cb35-131">Create a public IP address</span></span>
<span data-ttu-id="4cb35-132">tooaccess aplikacji na hello Internet, należy publicznego adresu IP dla modułu równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="4cb35-132">tooaccess your app on hello Internet, you need a public IP address for hello load balancer.</span></span> <span data-ttu-id="4cb35-133">Utwórz publiczny adres IP z [utworzyć az sieci publicznej ip](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="4cb35-133">Create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="4cb35-134">Witaj poniższy przykład tworzy publiczny adres IP o nazwie *myPublicIP* w hello *myResourceGroupLoadBalancer* grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="4cb35-134">hello following example creates a public IP address named *myPublicIP* in hello *myResourceGroupLoadBalancer* resource group:</span></span>

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="4cb35-135">Tworzenie modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="4cb35-135">Create a load balancer</span></span>
<span data-ttu-id="4cb35-136">Tworzenie modułu równoważenia obciążenia z [utworzyć równoważeniem obciążenia sieciowego az](/cli/azure/network/lb#create).</span><span class="sxs-lookup"><span data-stu-id="4cb35-136">Create a load balancer with [az network lb create](/cli/azure/network/lb#create).</span></span> <span data-ttu-id="4cb35-137">Witaj poniższy przykład tworzy moduł równoważenia obciążenia o nazwie *myLoadBalancer* i przypisuje hello *myPublicIP* konfiguracji IP frontonu toohello adresu:</span><span class="sxs-lookup"><span data-stu-id="4cb35-137">hello following example creates a load balancer named *myLoadBalancer* and assigns hello *myPublicIP* address toohello front-end IP configuration:</span></span>

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a><span data-ttu-id="4cb35-138">Utworzyć sondy kondycji</span><span class="sxs-lookup"><span data-stu-id="4cb35-138">Create a health probe</span></span>
<span data-ttu-id="4cb35-139">tooallow hello stanu usługi równoważenia obciążenia toomonitor hello aplikacji, możesz użyć sondy kondycji.</span><span class="sxs-lookup"><span data-stu-id="4cb35-139">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="4cb35-140">sondy kondycji Hello dynamicznie dodaje lub usuwa maszyn wirtualnych z obrotu usługi równoważenia obciążenia hello oparte na ich kontroli toohealth odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="4cb35-140">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="4cb35-141">Domyślnie maszyny Wirtualnej zostanie usunięte z dystrybucji modułu równoważenia obciążenia powitania po dwóch kolejnych błędów na 15 sekund.</span><span class="sxs-lookup"><span data-stu-id="4cb35-141">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="4cb35-142">Można utworzyć sondy kondycji, na podstawie protokołu lub stronę wyboru kondycji określonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4cb35-142">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="4cb35-143">Witaj poniższy przykład tworzy badanie TCP.</span><span class="sxs-lookup"><span data-stu-id="4cb35-143">hello following example creates a TCP probe.</span></span> <span data-ttu-id="4cb35-144">Można również utworzyć niestandardowe sond HTTP więcej kontroli kondycji szczegółowe.</span><span class="sxs-lookup"><span data-stu-id="4cb35-144">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="4cb35-145">Podczas korzystania z niestandardowego badanie HTTP, należy utworzyć hello strona sprawdzania kondycji, takich jak *healthcheck.js*.</span><span class="sxs-lookup"><span data-stu-id="4cb35-145">When using a custom HTTP probe, you must create hello health check page, such as *healthcheck.js*.</span></span> <span data-ttu-id="4cb35-146">Sonda Hello musi zwracać **HTTP 200 OK** odpowiedzi dla hosta usługi równoważenia obciążenia hello hello tookeep rotacji.</span><span class="sxs-lookup"><span data-stu-id="4cb35-146">hello probe must return an **HTTP 200 OK** response for hello load balancer tookeep hello host in rotation.</span></span>

<span data-ttu-id="4cb35-147">Użyj toocreate sondy kondycji TCP [utworzyć sondy równoważeniem obciążenia sieciowego az](/cli/azure/network/lb/probe#create).</span><span class="sxs-lookup"><span data-stu-id="4cb35-147">toocreate a TCP health probe, you use [az network lb probe create](/cli/azure/network/lb/probe#create).</span></span> <span data-ttu-id="4cb35-148">Witaj poniższy przykład tworzy badanie kondycji o nazwie *myHealthProbe*:</span><span class="sxs-lookup"><span data-stu-id="4cb35-148">hello following example creates a health probe named *myHealthProbe*:</span></span>

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="4cb35-149">Tworzenie reguły modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="4cb35-149">Create a load balancer rule</span></span>
<span data-ttu-id="4cb35-150">Reguły modułu równoważenia obciążenia jest używany toodefine sposób ruch jest rozproszonej toohello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="4cb35-150">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span> <span data-ttu-id="4cb35-151">Należy zdefiniować hello frontonu konfigurację adresu IP dla ruchu przychodzącego hello i hello zaplecza IP puli tooreceive hello ruchu, wraz z hello wymagane źródłowy i port docelowy.</span><span class="sxs-lookup"><span data-stu-id="4cb35-151">You define hello front-end IP configuration for hello incoming traffic and hello back-end IP pool tooreceive hello traffic, along with hello required source and destination port.</span></span> <span data-ttu-id="4cb35-152">toomake się, że tylko dobrej kondycji maszyn wirtualnych odbieranie ruchu, możesz również definiować toouse sondy kondycji hello.</span><span class="sxs-lookup"><span data-stu-id="4cb35-152">toomake sure only healthy VMs receive traffic, you also define hello health probe toouse.</span></span>

<span data-ttu-id="4cb35-153">Tworzenie reguły modułu równoważenia obciążenia z [utworzyć regułę równoważeniem obciążenia sieciowego az](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="4cb35-153">Create a load balancer rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="4cb35-154">Witaj poniższy przykład powoduje utworzenie reguły o nazwie *myLoadBalancerRule*, używa hello *myHealthProbe* badania kondycji i równoważy ruch na porcie *80*:</span><span class="sxs-lookup"><span data-stu-id="4cb35-154">hello following example creates a rule named *myLoadBalancerRule*, uses hello *myHealthProbe* health probe, and balances traffic on port *80*:</span></span>

```azurecli-interactive 
az network lb rule create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myLoadBalancerRule \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --probe-name myHealthProbe
```


## <a name="configure-virtual-network"></a><span data-ttu-id="4cb35-155">Konfigurowanie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="4cb35-155">Configure virtual network</span></span>
<span data-ttu-id="4cb35-156">Przed wdrożeniem niektórych maszyn wirtualnych i przetestować z usługi równoważenia, Utwórz hello obsługi zasobów sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4cb35-156">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="4cb35-157">Aby uzyskać więcej informacji o sieciach wirtualnych, zobacz hello [Zarządzanie sieciami wirtualnymi Azure](tutorial-virtual-network.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="4cb35-157">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="4cb35-158">Utwórz zasoby sieciowe</span><span class="sxs-lookup"><span data-stu-id="4cb35-158">Create network resources</span></span>
<span data-ttu-id="4cb35-159">Tworzenie sieci wirtualnej z [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="4cb35-159">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="4cb35-160">Witaj poniższy przykład tworzy sieć wirtualną o nazwie *myVnet* z podsiecią o nazwie *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="4cb35-160">hello following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

<span data-ttu-id="4cb35-161">tooadd sieciowej grupy zabezpieczeń, użyj [utworzyć nsg sieci az](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="4cb35-161">tooadd a network security group, you use [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="4cb35-162">Witaj poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="4cb35-162">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="4cb35-163">Tworzenie reguły grupy zabezpieczeń sieci z [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="4cb35-163">Create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="4cb35-164">Witaj poniższy przykład tworzy regułę grupy zabezpieczeń sieci o nazwie *myNetworkSecurityGroupRule*:</span><span class="sxs-lookup"><span data-stu-id="4cb35-164">hello following example creates a network security group rule named *myNetworkSecurityGroupRule*:</span></span>

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

<span data-ttu-id="4cb35-165">Wirtualne karty sieciowe są tworzone za pomocą [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="4cb35-165">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="4cb35-166">Witaj poniższy przykład tworzy trzy wirtualne karty sieciowe.</span><span class="sxs-lookup"><span data-stu-id="4cb35-166">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="4cb35-167">(Jedną wirtualną kartę Sieciową dla każdej maszyny Wirtualnej można utworzyć dla aplikacji w hello następujące kroki).</span><span class="sxs-lookup"><span data-stu-id="4cb35-167">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="4cb35-168">Można tworzyć dodatkowe wirtualne karty sieciowe i maszyn wirtualnych w dowolnym momencie i dodać je toohello usługi równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="4cb35-168">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupLoadBalancer \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --network-security-group myNetworkSecurityGroup \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-virtual-machines"></a><span data-ttu-id="4cb35-169">Tworzenie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="4cb35-169">Create virtual machines</span></span>

### <a name="create-cloud-init-config"></a><span data-ttu-id="4cb35-170">Tworzenie konfiguracji init chmury</span><span class="sxs-lookup"><span data-stu-id="4cb35-170">Create cloud-init config</span></span>
<span data-ttu-id="4cb35-171">W poprzednim samouczek dotyczący [jak toocustomize maszyny wirtualnej systemu Linux, po pierwszym uruchomieniu komputera](tutorial-automate-vm-deployment.md), możesz przedstawiono sposób dostosowywania maszyny Wirtualnej tooautomate z inicjowaniem chmury.</span><span class="sxs-lookup"><span data-stu-id="4cb35-171">In a previous tutorial on [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with cloud-init.</span></span> <span data-ttu-id="4cb35-172">Można użyć tej samej chmurze inicjowania konfiguracji pliku tooinstall NGINX hello i uruchom prostej aplikacji Node.js "Hello World".</span><span class="sxs-lookup"><span data-stu-id="4cb35-172">You can use hello same cloud-init configuration file tooinstall NGINX and run a simple 'Hello World' Node.js app.</span></span>

<span data-ttu-id="4cb35-173">W bieżącym powłoki, Utwórz plik o nazwie *init.txt chmury* i Wklej powitania po konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4cb35-173">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="4cb35-174">Na przykład utworzyć plik hello w hello powłoki chmury nie na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="4cb35-174">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="4cb35-175">Wprowadź `sensible-editor cloud-init.txt` toocreate hello pliku i wyświetlić listę dostępnych edytory.</span><span class="sxs-lookup"><span data-stu-id="4cb35-175">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="4cb35-176">Upewnij się, że plik całego init chmury hello został poprawnie skopiowany, szczególnie hello pierwszy wiersz:</span><span class="sxs-lookup"><span data-stu-id="4cb35-176">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-virtual-machines"></a><span data-ttu-id="4cb35-177">Tworzenie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="4cb35-177">Create virtual machines</span></span>
<span data-ttu-id="4cb35-178">tooimprove hello wysoką dostępność aplikacji, umieść maszyn wirtualnych w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="4cb35-178">tooimprove hello high availability of your app, place your VMs in an availability set.</span></span> <span data-ttu-id="4cb35-179">Aby uzyskać więcej informacji na temat zestawów dostępności, zobacz poprzednie hello [jak maszyn wirtualnych o wysokiej dostępności toocreate](tutorial-availability-sets.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="4cb35-179">For more information about availability sets, see hello previous [How toocreate highly available virtual machines](tutorial-availability-sets.md) tutorial.</span></span>

<span data-ttu-id="4cb35-180">Utwórz zestaw o dostępności [tworzenia maszyny wirtualnej az zestawu dostępności](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="4cb35-180">Create an availability set with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="4cb35-181">Witaj poniższy przykład tworzy zbiór nazwanego dostępności *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="4cb35-181">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

<span data-ttu-id="4cb35-182">Teraz można tworzyć maszyn wirtualnych hello o [tworzenia maszyny wirtualnej az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="4cb35-182">Now you can create hello VMs with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="4cb35-183">Witaj poniższy przykład tworzy trzech maszyn wirtualnych i generuje klucze SSH, jeśli jeszcze nie istnieje:</span><span class="sxs-lookup"><span data-stu-id="4cb35-183">hello following example creates three VMs and generates SSH keys if they do not already exist:</span></span>

```bash
for i in `seq 1 3`; do
    az vm create \
        --resource-group myResourceGroupLoadBalancer \
        --name myVM$i \
        --availability-set myAvailabilitySet \
        --nics myNic$i \
        --image UbuntuLTS \
        --admin-username azureuser \
        --generate-ssh-keys \
        --custom-data cloud-init.txt \
        --no-wait
done
```

<span data-ttu-id="4cb35-184">Istnieją zadania w tle, które nadal toorun po hello Azure CLI zwraca toohello wiersza.</span><span class="sxs-lookup"><span data-stu-id="4cb35-184">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="4cb35-185">Witaj `--no-wait` parametru nie oczekuje dla wszystkich hello toocomplete zadania.</span><span class="sxs-lookup"><span data-stu-id="4cb35-185">hello `--no-wait` parameter does not wait for all hello tasks toocomplete.</span></span> <span data-ttu-id="4cb35-186">Może to być inny kilka minut, w celu uzyskania dostępu do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="4cb35-186">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="4cb35-187">Witaj sondy kondycji modułu równoważenia obciążenia automatycznie wykrywa aplikacji hello jest uruchomiona na każdej maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4cb35-187">hello load balancer health probe automatically detects when hello app is running on each VM.</span></span> <span data-ttu-id="4cb35-188">Po uruchomieniu aplikacji hello reguły modułu równoważenia obciążenia hello uruchamia toodistribute ruchu.</span><span class="sxs-lookup"><span data-stu-id="4cb35-188">Once hello app is running, hello load balancer rule starts toodistribute traffic.</span></span>


## <a name="test-load-balancer"></a><span data-ttu-id="4cb35-189">Test usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="4cb35-189">Test load balancer</span></span>
<span data-ttu-id="4cb35-190">Uzyskaj hello publicznego adresu IP z usługi równoważenia obciążenia z [az sieci ip publicznego Pokaż](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="4cb35-190">Obtain hello public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="4cb35-191">Witaj poniższy przykład uzyskuje hello adres IP dla *myPublicIP* utworzony wcześniej:</span><span class="sxs-lookup"><span data-stu-id="4cb35-191">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="4cb35-192">W przeglądarce sieci web tooa można następnie wprowadzić hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="4cb35-192">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="4cb35-193">Pamiętaj — zajmuje kilka minut hello hello maszyn wirtualnych toobe gotowe przed toothem ruchu toodistribute rozpoczyna się hello modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="4cb35-193">Remember - it takes a few minutes hello hello VMs toobe ready before hello load balancer starts toodistribute traffic toothem.</span></span> <span data-ttu-id="4cb35-194">Aplikacja Hello jest wyświetlana, łącznie z nazwą hosta hello hello maszyny Wirtualnej tego modułu równoważenia obciążenia hello rozproszonych tooas ruchu w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="4cb35-194">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Uruchomionej aplikacji Node.js](./media/tutorial-load-balancer/running-nodejs-app.png)

<span data-ttu-id="4cb35-196">Moduł równoważenia obciążenia hello toosee Dystrybuuj ruch we wszystkich trzech maszyn wirtualnych z tą aplikacją, użytkownik może życie odświeżania przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="4cb35-196">toosee hello load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="4cb35-197">Dodawanie i usuwanie maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="4cb35-197">Add and remove VMs</span></span>
<span data-ttu-id="4cb35-198">Może być konieczne tooperform konserwacji na powitania maszyn wirtualnych z tą aplikacją, takich jak instalowanie aktualizacji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="4cb35-198">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="4cb35-199">toodeal z aplikacją tooyour zwiększenie obciążenia, może być konieczne tooadd kolejnych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="4cb35-199">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="4cb35-200">W tej sekcji opisano sposób tooremove lub dodać maszyny Wirtualnej z hello modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="4cb35-200">This section shows you how tooremove or add a VM from hello load balancer.</span></span>

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="4cb35-201">Usuń Maszynę wirtualną z hello modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="4cb35-201">Remove a VM from hello load balancer</span></span>
<span data-ttu-id="4cb35-202">Możesz usunąć Maszynę wirtualną z puli adresów zaplecza hello z [az kart konfiguracji ip puli adresów sieciowych — Usuń](/cli/azure/network/nic/ip-config/address-pool#remove).</span><span class="sxs-lookup"><span data-stu-id="4cb35-202">You can remove a VM from hello backend address pool with [az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove).</span></span> <span data-ttu-id="4cb35-203">następujące przykładowe usuwa Hello hello wirtualnej karty Sieciowej dla **myVM2** z *myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="4cb35-203">hello following example removes hello virtual NIC for **myVM2** from *myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

<span data-ttu-id="4cb35-204">Moduł równoważenia obciążenia hello toosee rozpowszechniają ruchu hello dwóch pozostałych maszyn wirtualnych z tą aplikacją możesz można życie odświeżania przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="4cb35-204">toosee hello load balancer distribute traffic across hello remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="4cb35-205">Teraz można przeprowadzać konserwacji na powitania maszynę Wirtualną, takie jak instalowanie aktualizacji systemu operacyjnego lub wykonywania ponownego uruchomienia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4cb35-205">You can now perform maintenance on hello VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="4cb35-206">Dodaj usługi równoważenia obciążenia toohello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="4cb35-206">Add a VM toohello load balancer</span></span>
<span data-ttu-id="4cb35-207">Po wykonaniu obsługi maszyny Wirtualnej lub tooexpand pojemności, należy dodać pula adresów zaplecza toohello maszyny Wirtualnej z [az kart konfiguracji ip puli adresów sieciowych — Dodaj](/cli/azure/network/nic/ip-config/address-pool#add).</span><span class="sxs-lookup"><span data-stu-id="4cb35-207">After performing VM maintenance, or if you need tooexpand capacity, you can add a VM toohello backend address pool with [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add).</span></span> <span data-ttu-id="4cb35-208">Witaj poniższy przykład umożliwia dodanie hello wirtualnej karty Sieciowej dla **myVM2** za*myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="4cb35-208">hello following example adds hello virtual NIC for **myVM2** too*myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a><span data-ttu-id="4cb35-209">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4cb35-209">Next steps</span></span>
<span data-ttu-id="4cb35-210">W tym samouczku utworzony moduł równoważenia obciążenia i dołączyć tooit maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="4cb35-210">In this tutorial, you created a load balancer and attached VMs tooit.</span></span> <span data-ttu-id="4cb35-211">W tym samouczku omówiono:</span><span class="sxs-lookup"><span data-stu-id="4cb35-211">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4cb35-212">Tworzenie usługi równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="4cb35-212">Create an Azure load balancer</span></span>
> * <span data-ttu-id="4cb35-213">Utwórz kondycji sondę modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="4cb35-213">Create a load balancer health probe</span></span>
> * <span data-ttu-id="4cb35-214">Tworzenie reguły ruchu usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="4cb35-214">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="4cb35-215">Użyj toocreate init chmury podstawowej aplikacji Node.js</span><span class="sxs-lookup"><span data-stu-id="4cb35-215">Use cloud-init toocreate a basic Node.js app</span></span>
> * <span data-ttu-id="4cb35-216">Tworzenie maszyn wirtualnych i Dołącz tooa modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="4cb35-216">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="4cb35-217">Wyświetl modułu równoważenia obciążenia w akcji</span><span class="sxs-lookup"><span data-stu-id="4cb35-217">View a load balancer in action</span></span>
> * <span data-ttu-id="4cb35-218">Dodawanie i usuwanie maszyny wirtualne z modułem równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="4cb35-218">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="4cb35-219">Więcej informacji na temat składników sieci wirtualnej platformy Azure poprawić toohello dalej toolearn samouczka.</span><span class="sxs-lookup"><span data-stu-id="4cb35-219">Advance toohello next tutorial toolearn more about Azure virtual network components.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4cb35-220">Zarządzanie maszynami wirtualnymi i sieciami wirtualnymi</span><span class="sxs-lookup"><span data-stu-id="4cb35-220">Manage VMs and virtual networks</span></span>](tutorial-virtual-network.md)
