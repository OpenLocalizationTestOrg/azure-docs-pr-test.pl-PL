---
title: "Jak załadować saldo maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać usługi równoważenia obciążenia Azure do tworzenia aplikacji wysokiej dostępności i bezpieczne w trzech maszyn wirtualnych systemu Linux"
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
ms.openlocfilehash: 7b3a089d2f6386afcc46cbc4377594be0d758fc6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-load-balance-linux-virtual-machines-in-azure-to-create-a-highly-available-application"></a><span data-ttu-id="9cb94-103">Jak załadować saldo maszyn wirtualnych systemu Linux na platformie Azure, aby utworzyć aplikację wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="9cb94-103">How to load balance Linux virtual machines in Azure to create a highly available application</span></span>
<span data-ttu-id="9cb94-104">Równoważenie obciążenia sieciowego zapewnia wyższy poziom dostępności dzięki rozproszeniu przychodzące żądania między wieloma maszynami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="9cb94-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="9cb94-105">W tym samouczku opisano różne składniki usługi równoważenia obciążenia Azure dystrybucji ruchu, które zapewniają wysoką dostępność.</span><span class="sxs-lookup"><span data-stu-id="9cb94-105">In this tutorial, you learn about the different components of the Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="9cb94-106">Omawiane kwestie:</span><span class="sxs-lookup"><span data-stu-id="9cb94-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9cb94-107">Tworzenie usługi równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="9cb94-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="9cb94-108">Utwórz kondycji sondę modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="9cb94-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="9cb94-109">Tworzenie reguły ruchu usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="9cb94-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="9cb94-110">Umożliwia utworzenie podstawowej aplikacji Node.js init chmury</span><span class="sxs-lookup"><span data-stu-id="9cb94-110">Use cloud-init to create a basic Node.js app</span></span>
> * <span data-ttu-id="9cb94-111">Tworzenie maszyn wirtualnych i dołączanie do usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="9cb94-111">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="9cb94-112">Wyświetl modułu równoważenia obciążenia w akcji</span><span class="sxs-lookup"><span data-stu-id="9cb94-112">View a load balancer in action</span></span>
> * <span data-ttu-id="9cb94-113">Dodawanie i usuwanie maszyny wirtualne z modułem równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="9cb94-113">Add and remove VMs from a load balancer</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9cb94-114">Jeśli wybierzesz do zainstalowania i używania interfejsu wiersza polecenia lokalnie, w tym samouczku wymaga używasz interfejsu wiersza polecenia Azure w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="9cb94-114">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9cb94-115">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="9cb94-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="9cb94-116">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9cb94-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="azure-load-balancer-overview"></a><span data-ttu-id="9cb94-117">Omówienie usługi równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="9cb94-117">Azure load balancer overview</span></span>
<span data-ttu-id="9cb94-118">Moduł równoważenia obciążenia Azure jest równoważenia obciążenia warstwy 4 (TCP, UDP), który zapewnia wysoką dostępność, przekazując przychodzący ruch między maszynami wirtualnymi w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="9cb94-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="9cb94-119">Badanie kondycji modułu równoważenia obciążenia monitoruje danego portu na każdej maszynie Wirtualnej i tylko dystrybuuje ruch do operacyjnej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9cb94-119">A load balancer health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span>

<span data-ttu-id="9cb94-120">Należy zdefiniować frontonu konfiguracji adresu IP, który zawiera co najmniej jeden publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="9cb94-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="9cb94-121">Ta frontonu konfiguracji IP umożliwia Twojej usługi równoważenia obciążenia i aplikacje mają być dostępne za pośrednictwem Internetu.</span><span class="sxs-lookup"><span data-stu-id="9cb94-121">This front-end IP configuration allows your load balancer and applications to be accessible over the Internet.</span></span> 

<span data-ttu-id="9cb94-122">Maszyny wirtualne połączenia z modułem równoważenia obciążenia przy użyciu ich karty interfejsu sieci wirtualnej (NIC).</span><span class="sxs-lookup"><span data-stu-id="9cb94-122">Virtual machines connect to a load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="9cb94-123">Aby rozpowszechnić ruch do maszyn wirtualnych, puli adresów zaplecza zawiera adres IP adresów wirtualnych (NIC) połączony z usługą równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="9cb94-123">To distribute traffic to the VMs, a back-end address pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span></span>

<span data-ttu-id="9cb94-124">Aby sterowanie przepływem ruchu, należy zdefiniować reguły modułu równoważenia obciążenia dla określonych portów i protokołów, które mapują do maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="9cb94-124">To control the flow of traffic, you define load balancer rules for specific ports and protocols that map to your VMs.</span></span>

<span data-ttu-id="9cb94-125">Po wykonaniu poprzednich w samouczku [utworzyć zestaw skali maszyny wirtualnej](tutorial-create-vmss.md), usługi równoważenia obciążenia został utworzony.</span><span class="sxs-lookup"><span data-stu-id="9cb94-125">If you followed the previous tutorial to [create a virtual machine scale set](tutorial-create-vmss.md), a load balancer was created for you.</span></span> <span data-ttu-id="9cb94-126">Wszystkie te składniki zostały skonfigurowane dla Ciebie jako część zestawu skali.</span><span class="sxs-lookup"><span data-stu-id="9cb94-126">All these components were configured for you as part of the scale set.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="9cb94-127">Tworzenie usługi równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="9cb94-127">Create Azure load balancer</span></span>
<span data-ttu-id="9cb94-128">W tej sekcji Szczegóły, jak można tworzyć i konfigurować poszczególnych składników usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="9cb94-128">This section details how you can create and configure each component of the load balancer.</span></span> <span data-ttu-id="9cb94-129">Przed utworzeniem przez moduł równoważenia obciążenia, Utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="9cb94-129">Before you can create your load balancer, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="9cb94-130">Poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupLoadBalancer* w *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="9cb94-130">The following example creates a resource group named *myResourceGroupLoadBalancer* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="9cb94-131">Tworzenie publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="9cb94-131">Create a public IP address</span></span>
<span data-ttu-id="9cb94-132">Aby uzyskać dostęp do aplikacji w Internecie, należy publicznego adresu IP usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="9cb94-132">To access your app on the Internet, you need a public IP address for the load balancer.</span></span> <span data-ttu-id="9cb94-133">Utwórz publiczny adres IP z [utworzyć az sieci publicznej ip](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="9cb94-133">Create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="9cb94-134">Poniższy przykład tworzy publiczny adres IP o nazwie *myPublicIP* w *myResourceGroupLoadBalancer* grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="9cb94-134">The following example creates a public IP address named *myPublicIP* in the *myResourceGroupLoadBalancer* resource group:</span></span>

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="9cb94-135">Tworzenie modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="9cb94-135">Create a load balancer</span></span>
<span data-ttu-id="9cb94-136">Tworzenie modułu równoważenia obciążenia z [utworzyć równoważeniem obciążenia sieciowego az](/cli/azure/network/lb#create).</span><span class="sxs-lookup"><span data-stu-id="9cb94-136">Create a load balancer with [az network lb create](/cli/azure/network/lb#create).</span></span> <span data-ttu-id="9cb94-137">Poniższy przykład tworzy moduł równoważenia obciążenia o nazwie *myLoadBalancer* i przypisuje *myPublicIP* adres frontonu konfiguracją protokołu IP:</span><span class="sxs-lookup"><span data-stu-id="9cb94-137">The following example creates a load balancer named *myLoadBalancer* and assigns the *myPublicIP* address to the front-end IP configuration:</span></span>

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a><span data-ttu-id="9cb94-138">Utworzyć sondy kondycji</span><span class="sxs-lookup"><span data-stu-id="9cb94-138">Create a health probe</span></span>
<span data-ttu-id="9cb94-139">Aby zezwolić usłudze równoważenia obciążenia do monitorowania stanu aplikacji, należy użyć sondy kondycji.</span><span class="sxs-lookup"><span data-stu-id="9cb94-139">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="9cb94-140">Sondy kondycji dynamicznie dodaje lub usuwa maszyn wirtualnych z oparte na ich odpowiedzi na sprawdzenie kondycji obrót usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="9cb94-140">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="9cb94-141">Domyślnie maszyny Wirtualnej zostanie usunięte z dystrybucji modułu równoważenia obciążenia po dwóch kolejnych błędów na 15 sekund.</span><span class="sxs-lookup"><span data-stu-id="9cb94-141">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="9cb94-142">Można utworzyć sondy kondycji, na podstawie protokołu lub stronę wyboru kondycji określonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9cb94-142">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="9cb94-143">Poniższy przykład tworzy sondowaniem TCP.</span><span class="sxs-lookup"><span data-stu-id="9cb94-143">The following example creates a TCP probe.</span></span> <span data-ttu-id="9cb94-144">Można również utworzyć niestandardowe sond HTTP więcej kontroli kondycji szczegółowe.</span><span class="sxs-lookup"><span data-stu-id="9cb94-144">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="9cb94-145">Podczas korzystania z niestandardowego badanie HTTP, należy utworzyć strona sprawdzania kondycji, takich jak *healthcheck.js*.</span><span class="sxs-lookup"><span data-stu-id="9cb94-145">When using a custom HTTP probe, you must create the health check page, such as *healthcheck.js*.</span></span> <span data-ttu-id="9cb94-146">Sonda musi zwracać **HTTP 200 OK** odpowiedzi dla usługi równoważenia obciążenia zachować hosta w obrotu.</span><span class="sxs-lookup"><span data-stu-id="9cb94-146">The probe must return an **HTTP 200 OK** response for the load balancer to keep the host in rotation.</span></span>

<span data-ttu-id="9cb94-147">Aby utworzyć sondy kondycji TCP, należy użyć [utworzyć sondy równoważeniem obciążenia sieciowego az](/cli/azure/network/lb/probe#create).</span><span class="sxs-lookup"><span data-stu-id="9cb94-147">To create a TCP health probe, you use [az network lb probe create](/cli/azure/network/lb/probe#create).</span></span> <span data-ttu-id="9cb94-148">Poniższy przykład tworzy badanie kondycji o nazwie *myHealthProbe*:</span><span class="sxs-lookup"><span data-stu-id="9cb94-148">The following example creates a health probe named *myHealthProbe*:</span></span>

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="9cb94-149">Tworzenie reguły modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="9cb94-149">Create a load balancer rule</span></span>
<span data-ttu-id="9cb94-150">Reguły modułu równoważenia obciążenia jest używany do definiowania rozkład ruchu do maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="9cb94-150">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span> <span data-ttu-id="9cb94-151">Należy zdefiniować konfiguracji IP frontonu dla ruchu przychodzącego i puli adresów IP zaplecza, aby odbierać ruch, wraz z wymagany port źródłowy i docelowy.</span><span class="sxs-lookup"><span data-stu-id="9cb94-151">You define the front-end IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span></span> <span data-ttu-id="9cb94-152">Aby upewnij się, że tylko dobrej kondycji maszyn wirtualnych odbieranie ruchu, również zdefiniować sondy kondycji do użycia.</span><span class="sxs-lookup"><span data-stu-id="9cb94-152">To make sure only healthy VMs receive traffic, you also define the health probe to use.</span></span>

<span data-ttu-id="9cb94-153">Tworzenie reguły modułu równoważenia obciążenia z [utworzyć regułę równoważeniem obciążenia sieciowego az](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="9cb94-153">Create a load balancer rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="9cb94-154">Poniższy przykład tworzy reguły o nazwie *myLoadBalancerRule*, używa *myHealthProbe* badania kondycji i równoważy ruch na porcie *80*:</span><span class="sxs-lookup"><span data-stu-id="9cb94-154">The following example creates a rule named *myLoadBalancerRule*, uses the *myHealthProbe* health probe, and balances traffic on port *80*:</span></span>

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


## <a name="configure-virtual-network"></a><span data-ttu-id="9cb94-155">Skonfiguruj sieć wirtualną</span><span class="sxs-lookup"><span data-stu-id="9cb94-155">Configure virtual network</span></span>
<span data-ttu-id="9cb94-156">Przed wdrożeniem niektórych maszyn wirtualnych i przetestować z usługi równoważenia, Utwórz pomocnicze zasoby sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9cb94-156">Before you deploy some VMs and can test your balancer, create the supporting virtual network resources.</span></span> <span data-ttu-id="9cb94-157">Aby uzyskać więcej informacji o sieciach wirtualnych, zobacz [Zarządzanie sieciami wirtualnymi Azure](tutorial-virtual-network.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="9cb94-157">For more information about virtual networks, see the [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="9cb94-158">Utwórz zasoby sieciowe</span><span class="sxs-lookup"><span data-stu-id="9cb94-158">Create network resources</span></span>
<span data-ttu-id="9cb94-159">Tworzenie sieci wirtualnej z [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="9cb94-159">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="9cb94-160">Poniższy przykład tworzy sieć wirtualną o nazwie *myVnet* z podsiecią o nazwie *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="9cb94-160">The following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

<span data-ttu-id="9cb94-161">Aby dodać grupę zabezpieczeń sieci, należy użyć [utworzyć nsg sieci az](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="9cb94-161">To add a network security group, you use [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="9cb94-162">Poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="9cb94-162">The following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="9cb94-163">Tworzenie reguły grupy zabezpieczeń sieci z [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="9cb94-163">Create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="9cb94-164">Poniższy przykład tworzy regułę grupy zabezpieczeń sieci o nazwie *myNetworkSecurityGroupRule*:</span><span class="sxs-lookup"><span data-stu-id="9cb94-164">The following example creates a network security group rule named *myNetworkSecurityGroupRule*:</span></span>

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

<span data-ttu-id="9cb94-165">Wirtualne karty sieciowe są tworzone za pomocą [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="9cb94-165">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="9cb94-166">Poniższy przykład tworzy trzy wirtualne karty sieciowe.</span><span class="sxs-lookup"><span data-stu-id="9cb94-166">The following example creates three virtual NICs.</span></span> <span data-ttu-id="9cb94-167">(Jedną wirtualną kartę Sieciową dla każdej maszyny Wirtualnej można utworzyć dla aplikacji w poniższych krokach).</span><span class="sxs-lookup"><span data-stu-id="9cb94-167">(One virtual NIC for each VM you create for your app in the following steps).</span></span> <span data-ttu-id="9cb94-168">Można utworzyć dodatkowe wirtualne karty sieciowe i maszyn wirtualnych w dowolnym momencie i dodaj je do usługi równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="9cb94-168">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span></span>

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

## <a name="create-virtual-machines"></a><span data-ttu-id="9cb94-169">Tworzenie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="9cb94-169">Create virtual machines</span></span>

### <a name="create-cloud-init-config"></a><span data-ttu-id="9cb94-170">Tworzenie konfiguracji init chmury</span><span class="sxs-lookup"><span data-stu-id="9cb94-170">Create cloud-init config</span></span>
<span data-ttu-id="9cb94-171">W poprzednich samouczek dotyczący [sposobu dostosowywania maszyny wirtualnej systemu Linux, po pierwszym uruchomieniu komputera](tutorial-automate-vm-deployment.md), wiesz, jak można zautomatyzować dostosowania maszyny Wirtualnej z inicjowaniem chmury.</span><span class="sxs-lookup"><span data-stu-id="9cb94-171">In a previous tutorial on [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how to automate VM customization with cloud-init.</span></span> <span data-ttu-id="9cb94-172">Można użyć tego samego pliku konfiguracji chmury init NGINX zainstalować i uruchomić prostej aplikacji Node.js "Hello World".</span><span class="sxs-lookup"><span data-stu-id="9cb94-172">You can use the same cloud-init configuration file to install NGINX and run a simple 'Hello World' Node.js app.</span></span>

<span data-ttu-id="9cb94-173">W bieżącym powłoki, Utwórz plik o nazwie *init.txt chmury* i wklej następującą konfigurację.</span><span class="sxs-lookup"><span data-stu-id="9cb94-173">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="9cb94-174">Na przykład utworzyć plik, w powłoce chmury nie na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="9cb94-174">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="9cb94-175">Wprowadź `sensible-editor cloud-init.txt` do tworzenia pliku i wyświetlić listę dostępnych edytory.</span><span class="sxs-lookup"><span data-stu-id="9cb94-175">Enter `sensible-editor cloud-init.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="9cb94-176">Upewnij się, że poprawnie skopiować pliku całego init chmury szczególnie pierwszy wiersz:</span><span class="sxs-lookup"><span data-stu-id="9cb94-176">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

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

### <a name="create-virtual-machines"></a><span data-ttu-id="9cb94-177">Tworzenie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="9cb94-177">Create virtual machines</span></span>
<span data-ttu-id="9cb94-178">Aby zwiększyć wysoką dostępność aplikacji, umieść maszyn wirtualnych w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="9cb94-178">To improve the high availability of your app, place your VMs in an availability set.</span></span> <span data-ttu-id="9cb94-179">Aby uzyskać więcej informacji na temat zestawów dostępności, zobacz poprzedni [sposób tworzenia maszyn wirtualnych o wysokiej dostępności](tutorial-availability-sets.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="9cb94-179">For more information about availability sets, see the previous [How to create highly available virtual machines](tutorial-availability-sets.md) tutorial.</span></span>

<span data-ttu-id="9cb94-180">Utwórz zestaw o dostępności [tworzenia maszyny wirtualnej az zestawu dostępności](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="9cb94-180">Create an availability set with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="9cb94-181">Poniższy przykład tworzy zbiór nazwanego dostępności *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="9cb94-181">The following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

<span data-ttu-id="9cb94-182">Teraz można tworzyć maszyn wirtualnych o [tworzenia maszyny wirtualnej az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="9cb94-182">Now you can create the VMs with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="9cb94-183">Poniższy przykład tworzy trzech maszyn wirtualnych i generuje klucze SSH, jeśli jeszcze nie istnieje:</span><span class="sxs-lookup"><span data-stu-id="9cb94-183">The following example creates three VMs and generates SSH keys if they do not already exist:</span></span>

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

<span data-ttu-id="9cb94-184">Istnieją zadania w tle, które nadal działać po interfejsu wiersza polecenia Azure powrót do wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="9cb94-184">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="9cb94-185">`--no-wait` Parametr bez oczekiwania na ukończenie wszystkich zadań.</span><span class="sxs-lookup"><span data-stu-id="9cb94-185">The `--no-wait` parameter does not wait for all the tasks to complete.</span></span> <span data-ttu-id="9cb94-186">Może to być inny kilka minut, w celu uzyskania dostępu do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9cb94-186">It may be another couple of minutes before you can access the app.</span></span> <span data-ttu-id="9cb94-187">Sondy kondycji modułu równoważenia obciążenia automatycznie wykrywa, gdy aplikacja jest uruchomiona na każdej maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9cb94-187">The load balancer health probe automatically detects when the app is running on each VM.</span></span> <span data-ttu-id="9cb94-188">Gdy aplikacja jest uruchomiona, rozpoczyna się reguły modułu równoważenia obciążenia do dystrybucji ruchu.</span><span class="sxs-lookup"><span data-stu-id="9cb94-188">Once the app is running, the load balancer rule starts to distribute traffic.</span></span>


## <a name="test-load-balancer"></a><span data-ttu-id="9cb94-189">Test usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="9cb94-189">Test load balancer</span></span>
<span data-ttu-id="9cb94-190">Publiczny adres IP z usługi równoważenia obciążenia z [az sieci ip publicznego Pokaż](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="9cb94-190">Obtain the public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="9cb94-191">Poniższy przykład uzyskuje adres IP dla *myPublicIP* utworzony wcześniej:</span><span class="sxs-lookup"><span data-stu-id="9cb94-191">The following example obtains the IP address for *myPublicIP* created earlier:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="9cb94-192">Następnie można wprowadzić publicznego adresu IP w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="9cb94-192">You can then enter the public IP address in to a web browser.</span></span> <span data-ttu-id="9cb94-193">Pamiętaj — zajmuje kilka minut maszyn wirtualnych będzie gotowa, przed rozpoczęciem dystrybucji ruchu do nich usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="9cb94-193">Remember - it takes a few minutes the the VMs to be ready before the load balancer starts to distribute traffic to them.</span></span> <span data-ttu-id="9cb94-194">Aplikacja jest wyświetlana, łącznie z nazwą hosta maszyny Wirtualnej dystrybuowanej usługi równoważenia obciążenia w ruchu, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="9cb94-194">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to as in the following example:</span></span>

![Uruchomionej aplikacji Node.js](./media/tutorial-load-balancer/running-nodejs-app.png)

<span data-ttu-id="9cb94-196">Aby wyświetlić Dystrybuuj ruch we wszystkich trzech maszyn wirtualnych z tą aplikacją usługi równoważenia obciążenia, możesz można życie odświeżania przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="9cb94-196">To see the load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="9cb94-197">Dodawanie i usuwanie maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="9cb94-197">Add and remove VMs</span></span>
<span data-ttu-id="9cb94-198">Może być konieczne przeprowadzenie konserwacji na maszynach wirtualnych z tą aplikacją, takich jak instalowanie aktualizacji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="9cb94-198">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="9cb94-199">Aby poradzić sobie z zwiększenie obciążenia do aplikacji, może być konieczne dodanie kolejnych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="9cb94-199">To deal with increased traffic to your app, you may need to add additional VMs.</span></span> <span data-ttu-id="9cb94-200">W tej sekcji przedstawiono sposób Usuń lub Dodaj Maszynę wirtualną z modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="9cb94-200">This section shows you how to remove or add a VM from the load balancer.</span></span>

### <a name="remove-a-vm-from-the-load-balancer"></a><span data-ttu-id="9cb94-201">Usuń Maszynę wirtualną z usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="9cb94-201">Remove a VM from the load balancer</span></span>
<span data-ttu-id="9cb94-202">Możesz usunąć Maszynę wirtualną z puli adresów zaplecza z [az kart konfiguracji ip puli adresów sieciowych — Usuń](/cli/azure/network/nic/ip-config/address-pool#remove).</span><span class="sxs-lookup"><span data-stu-id="9cb94-202">You can remove a VM from the backend address pool with [az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove).</span></span> <span data-ttu-id="9cb94-203">Poniższy przykład umożliwia usunięcie wirtualnej karty Sieciowej dla **myVM2** z *myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="9cb94-203">The following example removes the virtual NIC for **myVM2** from *myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

<span data-ttu-id="9cb94-204">Aby wyświetlić rozpowszechniają ruchu pozostałych dwóch maszyn wirtualnych z tą aplikacją usługi równoważenia obciążenia można można życie odświeżania przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="9cb94-204">To see the load balancer distribute traffic across the remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="9cb94-205">Teraz można przeprowadzać konserwacji na maszynie Wirtualnej, takie jak instalowanie aktualizacji systemu operacyjnego lub wykonywania ponownego uruchomienia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9cb94-205">You can now perform maintenance on the VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-to-the-load-balancer"></a><span data-ttu-id="9cb94-206">Dodaj Maszynę wirtualną z usługą równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="9cb94-206">Add a VM to the load balancer</span></span>
<span data-ttu-id="9cb94-207">Po wykonaniu obsługi maszyny Wirtualnej, lub jeśli trzeba zwiększyć pojemność, można dodać maszyny Wirtualnej do puli adresów zaplecza z [az kart konfiguracji ip puli adresów sieciowych — Dodaj](/cli/azure/network/nic/ip-config/address-pool#add).</span><span class="sxs-lookup"><span data-stu-id="9cb94-207">After performing VM maintenance, or if you need to expand capacity, you can add a VM to the backend address pool with [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add).</span></span> <span data-ttu-id="9cb94-208">W poniższym przykładzie dodano wirtualnej karty Sieciowej dla **myVM2** do *myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="9cb94-208">The following example adds the virtual NIC for **myVM2** to *myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a><span data-ttu-id="9cb94-209">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9cb94-209">Next steps</span></span>
<span data-ttu-id="9cb94-210">W tym samouczku utworzony moduł równoważenia obciążenia i dołączone do maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="9cb94-210">In this tutorial, you created a load balancer and attached VMs to it.</span></span> <span data-ttu-id="9cb94-211">Możesz przedstawiono sposób do:</span><span class="sxs-lookup"><span data-stu-id="9cb94-211">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9cb94-212">Tworzenie usługi równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="9cb94-212">Create an Azure load balancer</span></span>
> * <span data-ttu-id="9cb94-213">Utwórz kondycji sondę modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="9cb94-213">Create a load balancer health probe</span></span>
> * <span data-ttu-id="9cb94-214">Tworzenie reguły ruchu usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="9cb94-214">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="9cb94-215">Umożliwia utworzenie podstawowej aplikacji Node.js init chmury</span><span class="sxs-lookup"><span data-stu-id="9cb94-215">Use cloud-init to create a basic Node.js app</span></span>
> * <span data-ttu-id="9cb94-216">Tworzenie maszyn wirtualnych i dołączanie do usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="9cb94-216">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="9cb94-217">Wyświetl modułu równoważenia obciążenia w akcji</span><span class="sxs-lookup"><span data-stu-id="9cb94-217">View a load balancer in action</span></span>
> * <span data-ttu-id="9cb94-218">Dodawanie i usuwanie maszyny wirtualne z modułem równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="9cb94-218">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="9cb94-219">Przejdź do następnego samouczkiem, aby dowiedzieć się więcej o składnikach sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9cb94-219">Advance to the next tutorial to learn more about Azure virtual network components.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9cb94-220">Zarządzanie maszynami wirtualnymi i sieciami wirtualnymi</span><span class="sxs-lookup"><span data-stu-id="9cb94-220">Manage VMs and virtual networks</span></span>](tutorial-virtual-network.md)
