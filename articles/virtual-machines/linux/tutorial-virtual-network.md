---
title: Sieci wirtualnych platformy Azure i maszyn wirtualnych systemu Linux | Dokumentacja firmy Microsoft
description: "Samouczek — Zarządzanie sieciami wirtualnymi platformy Azure i maszyn wirtualnych systemu Linux z interfejsu wiersza polecenia platformy Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 2366905b8160675f77cbc41ba97540af70be8c01
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-the-azure-cli"></a><span data-ttu-id="04064-103">Zarządzanie sieciami wirtualnymi platformy Azure i maszyn wirtualnych systemu Linux z interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="04064-103">Manage Azure Virtual Networks and Linux Virtual Machines with the Azure CLI</span></span>

<span data-ttu-id="04064-104">Maszyny wirtualne platformy Azure używania sieci platformy Azure do komunikacji sieciowej wewnętrznych i zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="04064-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="04064-105">Ten samouczek przeprowadzi Cię przez wdrożenie dwóch maszyn wirtualnych i konfigurowanie sieci platformy Azure dla tych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="04064-105">This tutorial walks through deploying two virtual machines and configuring Azure networking for these VMs.</span></span> <span data-ttu-id="04064-106">Przykłady w tym samouczku założono, że maszyny wirtualne obsługujące aplikacji sieci web z bazy danych zaplecza, jednak aplikacja nie zostanie wdrożona w samouczku.</span><span class="sxs-lookup"><span data-stu-id="04064-106">The examples in this tutorial assume that the VMs are hosting a web application with a database back-end, however an application is not deployed in the tutorial.</span></span> <span data-ttu-id="04064-107">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="04064-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="04064-108">Wdrażanie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="04064-108">Deploy a virtual network</span></span>
> * <span data-ttu-id="04064-109">Utwórz podsieć sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="04064-109">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="04064-110">Dołącz do podsieci maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="04064-110">Attach virtual machines to a subnet</span></span>
> * <span data-ttu-id="04064-111">Zarządzanie publicznych adresów IP maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="04064-111">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="04064-112">Bezpieczny ruch przychodzący z Internetu</span><span class="sxs-lookup"><span data-stu-id="04064-112">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="04064-113">Bezpiecznej maszyny Wirtualnej do ruchu maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="04064-113">Secure VM to VM traffic</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="04064-114">Jeśli wybierzesz do zainstalowania i używania interfejsu wiersza polecenia lokalnie, w tym samouczku wymaga używasz interfejsu wiersza polecenia Azure w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="04064-114">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="04064-115">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="04064-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="04064-116">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="04064-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="vm-networking-overview"></a><span data-ttu-id="04064-117">Omówienie sieci maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="04064-117">VM networking overview</span></span>

<span data-ttu-id="04064-118">Sieci wirtualnych platformy Azure Włącz bezpiecznych połączeń sieci między maszynami wirtualnymi, internet i innymi usługami Azure, takich jak bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="04064-118">Azure virtual networks enable secure network connections between virtual machines, the internet, and other Azure services such as Azure SQL database.</span></span> <span data-ttu-id="04064-119">Sieci wirtualne są podzielone na segmentach logicznej podsieci.</span><span class="sxs-lookup"><span data-stu-id="04064-119">Virtual networks are broken down into logical segments called subnets.</span></span> <span data-ttu-id="04064-120">Podsieci są używane do sterowania przepływem sieci oraz funkcję granicy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="04064-120">Subnets are used to control network flow, and as a security boundary.</span></span> <span data-ttu-id="04064-121">Podczas wdrażania maszyny Wirtualnej, zwykle obejmuje interfejs sieci wirtualnej, który jest podłączony do podsieci.</span><span class="sxs-lookup"><span data-stu-id="04064-121">When deploying a VM, it generally includes a virtual network interface, which is attached to a subnet.</span></span>

## <a name="deploy-virtual-network"></a><span data-ttu-id="04064-122">Wdrażanie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="04064-122">Deploy virtual network</span></span>

<span data-ttu-id="04064-123">W tym samouczku jednej sieci wirtualnej jest tworzony z dwoma podsieciami.</span><span class="sxs-lookup"><span data-stu-id="04064-123">For this tutorial, a single virtual network is created with two subnets.</span></span> <span data-ttu-id="04064-124">Podsieci frontonu do obsługi aplikacji sieci web, a podsieć zaplecza dla hostingu serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="04064-124">A front-end subnet for hosting a web application, and a back-end subnet for hosting a database server.</span></span>

<span data-ttu-id="04064-125">Przed utworzeniem sieci wirtualnej, Utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="04064-125">Before you can create a virtual network, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="04064-126">Poniższy przykład tworzy grupę zasobów o nazwie *myRGNetwork* w lokalizacji eastus.</span><span class="sxs-lookup"><span data-stu-id="04064-126">The following example creates a resource group named *myRGNetwork* in the eastus location.</span></span>

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a><span data-ttu-id="04064-127">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="04064-127">Create virtual network</span></span>

<span data-ttu-id="04064-128">Nam [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create) polecenie, aby utworzyć sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="04064-128">Us the [az network vnet create](/cli/azure/network/vnet#create) command to create a virtual network.</span></span> <span data-ttu-id="04064-129">W tym przykładzie sieci o nazwie *mvVnet* i podano prefiksu adresu *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="04064-129">In this example, the network is named *mvVnet* and is given an address prefix of *10.0.0.0/16*.</span></span> <span data-ttu-id="04064-130">Tworzona jest również podsieć o nazwie *mySubnetFrontEnd* i prefiksem *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="04064-130">A subnet is also created with a name of *mySubnetFrontEnd* and a prefix of *10.0.1.0/24*.</span></span> <span data-ttu-id="04064-131">W dalszej części tego samouczka frontonu maszyny Wirtualnej jest podłączona do tej podsieci.</span><span class="sxs-lookup"><span data-stu-id="04064-131">Later in this tutorial a front-end VM is connected to this subnet.</span></span> 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a><span data-ttu-id="04064-132">Utwórz podsieć</span><span class="sxs-lookup"><span data-stu-id="04064-132">Create subnet</span></span>

<span data-ttu-id="04064-133">Nowa podsieć zostanie dodany do sieci wirtualnej przy użyciu [Utwórz podsieć sieci wirtualnej sieci az](/cli/azure/network/vnet/subnet#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="04064-133">A new subnet is added to the virtual network using the [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command.</span></span> <span data-ttu-id="04064-134">W tym przykładzie podsieć o nazwie *mySubnetBackEnd* i podano prefiksu adresu *10.0.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="04064-134">In this example, the subnet is named *mySubnetBackEnd* and is given an address prefix of *10.0.2.0/24*.</span></span> <span data-ttu-id="04064-135">Ta podsieć jest używany ze wszystkimi usługami zaplecza.</span><span class="sxs-lookup"><span data-stu-id="04064-135">This subnet is used with all back-end services.</span></span>

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

<span data-ttu-id="04064-136">W tym momencie sieci zostało utworzone i podzielone na dwie podsieci, jeden dla usługi frontonu i drugi dla usług zaplecza.</span><span class="sxs-lookup"><span data-stu-id="04064-136">At this point, a network has been created and segmented into two subnets, one for front-end services, and another for back-end services.</span></span> <span data-ttu-id="04064-137">W następnej sekcji maszyny wirtualne są tworzone i połączone z tych podsieci.</span><span class="sxs-lookup"><span data-stu-id="04064-137">In the next section, virtual machines are created and connected to these subnets.</span></span>

## <a name="understand-public-ip-address"></a><span data-ttu-id="04064-138">Zrozumienie publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="04064-138">Understand public IP address</span></span>

<span data-ttu-id="04064-139">Publiczny adres IP umożliwia zasobów platformy Azure jako dostępny w Internecie.</span><span class="sxs-lookup"><span data-stu-id="04064-139">A public IP address allows Azure resources to be accessible on the internet.</span></span> <span data-ttu-id="04064-140">W tej części samouczka tworzona jest maszyna wirtualna pokazują, jak pracować z publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="04064-140">In this section of the tutorial, a VM is created to demonstrate how to work with public IP addresses.</span></span>

### <a name="allocation-method"></a><span data-ttu-id="04064-141">Metoda alokacji</span><span class="sxs-lookup"><span data-stu-id="04064-141">Allocation method</span></span>

<span data-ttu-id="04064-142">Publiczny adres IP można przypisać jako dynamicznej lub statycznej.</span><span class="sxs-lookup"><span data-stu-id="04064-142">A public IP address can be allocated as either dynamic or static.</span></span> <span data-ttu-id="04064-143">Domyślnie dynamicznie przydzielane publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="04064-143">By default, public IP address dynamically allocated.</span></span> <span data-ttu-id="04064-144">Dynamiczne adresy IP są wydawane po cofnięciu przydziału maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="04064-144">Dynamic IP addresses are released when a VM is deallocated.</span></span> <span data-ttu-id="04064-145">Ten problem powoduje, że adres IP zmienić podczas żadnej operacji, która obejmuje dezalokacji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="04064-145">This behavior causes the IP address to change during any operation that includes a VM deallocation.</span></span>

<span data-ttu-id="04064-146">Metoda alokacji można ustawić pola statyczne, który zapewnia, że adres IP adres pozostają przypisane do maszyn wirtualnych, nawet podczas deallocated stanu.</span><span class="sxs-lookup"><span data-stu-id="04064-146">The allocation method can be set to static, which ensures that the IP address remain assigned to a VM, even during a deallocated state.</span></span> <span data-ttu-id="04064-147">Korzystając z statycznie przydzielony adres IP, nie można określić adres IP.</span><span class="sxs-lookup"><span data-stu-id="04064-147">When using a statically allocated IP address, the IP address itself cannot be specified.</span></span> <span data-ttu-id="04064-148">Zamiast tego jest ona przydzielone z puli dostępnych adresów.</span><span class="sxs-lookup"><span data-stu-id="04064-148">Instead, it is allocated from a pool of available addresses.</span></span>

### <a name="dynamic-allocation"></a><span data-ttu-id="04064-149">Dynamiczna alokacja</span><span class="sxs-lookup"><span data-stu-id="04064-149">Dynamic allocation</span></span>

<span data-ttu-id="04064-150">Podczas tworzenia maszyny Wirtualnej z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia domyślnego publicznego adresu IP adres metodę alokacji jest dynamiczny.</span><span class="sxs-lookup"><span data-stu-id="04064-150">When creating a VM with the [az vm create](/cli/azure/vm#create) command, the default public IP address allocation method is dynamic.</span></span> <span data-ttu-id="04064-151">W poniższym przykładzie zostanie utworzona maszyna wirtualna z dynamicznym adresem IP.</span><span class="sxs-lookup"><span data-stu-id="04064-151">In the following example, a VM is created with a dynamic IP address.</span></span> 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myFrontEndVM \
  --vnet-name myVnet \
  --subnet mySubnetFrontEnd \
  --nsg myNSGFrontEnd \
  --public-ip-address myFrontEndIP \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="static-allocation"></a><span data-ttu-id="04064-152">Statycznych alokacji</span><span class="sxs-lookup"><span data-stu-id="04064-152">Static allocation</span></span>

<span data-ttu-id="04064-153">Podczas tworzenia maszyny wirtualnej przy użyciu [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia, obejmują `--public-ip-address-allocation static` argument można przypisać statycznego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="04064-153">When creating a virtual machine using the [az vm create](/cli/azure/vm#create) command, include the `--public-ip-address-allocation static` argument to assign a static public IP address.</span></span> <span data-ttu-id="04064-154">Ta operacja nie jest prezentowana w tym samouczku, jednak w następnej sekcji dynamicznie przydzielonego adresu IP została zmieniona na statycznie przydzielonego adresu.</span><span class="sxs-lookup"><span data-stu-id="04064-154">This operation is not demonstrated in this tutorial, however in the next section a dynamically allocated IP address is changed to a statically allocated address.</span></span> 

### <a name="change-allocation-method"></a><span data-ttu-id="04064-155">Zmień metodę alokacji</span><span class="sxs-lookup"><span data-stu-id="04064-155">Change allocation method</span></span>

<span data-ttu-id="04064-156">Metoda alokacji adresów IP można zmienić za pomocą [az sieci ip publicznego aktualizacji](/cli/azure/network/public-ip#update) polecenia.</span><span class="sxs-lookup"><span data-stu-id="04064-156">The IP address allocation method can be changed using the [az network public-ip update](/cli/azure/network/public-ip#update) command.</span></span> <span data-ttu-id="04064-157">W tym przykładzie metoda alokacji adresu IP frontonu maszyny wirtualnej zostanie zmieniona na statyczne.</span><span class="sxs-lookup"><span data-stu-id="04064-157">In this example, the IP address allocation method of the front-end VM is changed to static.</span></span>

<span data-ttu-id="04064-158">Po pierwsze Cofnij Przydział maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="04064-158">First, deallocate the VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

<span data-ttu-id="04064-159">Użyj [az sieci ip publicznego aktualizacji](/cli/azure/network/public-ip#update) polecenie, aby zaktualizować metodę alokacji.</span><span class="sxs-lookup"><span data-stu-id="04064-159">Use the [az network public-ip update](/cli/azure/network/public-ip#update) command to update the allocation method.</span></span> <span data-ttu-id="04064-160">W takim przypadku `--allocation-method` jest ustawiany *statycznych*.</span><span class="sxs-lookup"><span data-stu-id="04064-160">In this case, the `--allocation-method` is being set to *static*.</span></span>

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

<span data-ttu-id="04064-161">Uruchom maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="04064-161">Start the VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a><span data-ttu-id="04064-162">Nie publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="04064-162">No public IP address</span></span>

<span data-ttu-id="04064-163">Często maszyny Wirtualnej nie musi być dostępny za pośrednictwem Internetu.</span><span class="sxs-lookup"><span data-stu-id="04064-163">Often, a VM does not need to be accessible over the internet.</span></span> <span data-ttu-id="04064-164">Aby utworzyć Maszynę wirtualną bez publicznego adresu IP, należy użyć `--public-ip-address ""` argumentu z pustego zestawu cudzysłowów.</span><span class="sxs-lookup"><span data-stu-id="04064-164">To create a VM without a public IP address, use the `--public-ip-address ""` argument with an empty set of double quotes.</span></span> <span data-ttu-id="04064-165">Ta konfiguracja jest przedstawiona w dalszej części tego samouczka</span><span class="sxs-lookup"><span data-stu-id="04064-165">This configuration is demonstrated later in this tutorial</span></span>

## <a name="secure-network-traffic"></a><span data-ttu-id="04064-166">Zabezpieczanie ruchu sieciowego</span><span class="sxs-lookup"><span data-stu-id="04064-166">Secure network traffic</span></span>

<span data-ttu-id="04064-167">Sieciowa grupa zabezpieczeń (NSG, network security group) zawiera listę reguł zabezpieczeń, które blokują lub zezwalają na ruch sieciowy do zasobów połączonych z usługami Azure Virtual Network (VNet).</span><span class="sxs-lookup"><span data-stu-id="04064-167">A network security group (NSG) contains a list of security rules that allow or deny network traffic to resources connected to Azure Virtual Networks (VNet).</span></span> <span data-ttu-id="04064-168">Grupy NSG można skojarzyć z podsieci lub sieci poszczególnych interfejsów.</span><span class="sxs-lookup"><span data-stu-id="04064-168">NSGs can be associated to subnets or individual network interfaces.</span></span> <span data-ttu-id="04064-169">Grupa NSG jest skojarzona z karty sieciowej, ma zastosowanie tylko skojarzonego VM.</span><span class="sxs-lookup"><span data-stu-id="04064-169">When an NSG is associated with a network interface, it applies only the associated VM.</span></span> <span data-ttu-id="04064-170">Jeśli sieciowa grupa zabezpieczeń jest skojarzona z podsiecią, te reguły są stosowane do wszystkich zasobów połączonych z tą podsiecią.</span><span class="sxs-lookup"><span data-stu-id="04064-170">When an NSG is associated to a subnet, the rules apply to all resources connected to the subnet.</span></span> 

### <a name="network-security-group-rules"></a><span data-ttu-id="04064-171">Reguły grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="04064-171">Network security group rules</span></span>

<span data-ttu-id="04064-172">Reguły NSG definiują portów sieciowych za pośrednictwem których ruch jest dozwolony lub niedozwolony.</span><span class="sxs-lookup"><span data-stu-id="04064-172">NSG rules define networking ports over which traffic is allowed or denied.</span></span> <span data-ttu-id="04064-173">Zasady mogą obejmować źródłowe i docelowe zakresów adresów IP tak, aby ruch jest kontrolowany między konkretnych systemów lub podsieci.</span><span class="sxs-lookup"><span data-stu-id="04064-173">The rules can include source and destination IP address ranges so that traffic is controlled between specific systems or subnets.</span></span> <span data-ttu-id="04064-174">Reguły NSG obejmują także priorytet (od 1 — i 4096).</span><span class="sxs-lookup"><span data-stu-id="04064-174">NSG rules also include a priority (between 1—and 4096).</span></span> <span data-ttu-id="04064-175">Reguły są sprawdzane według ważności.</span><span class="sxs-lookup"><span data-stu-id="04064-175">Rules are evaluated in the order of priority.</span></span> <span data-ttu-id="04064-176">Reguła o priorytecie 100 jest oceniane przed regułą z priorytetem 200.</span><span class="sxs-lookup"><span data-stu-id="04064-176">A rule with a priority of 100 is evaluated before a rule with priority 200.</span></span>

<span data-ttu-id="04064-177">Wszystkie sieciowe grupy zabezpieczeń zawierają zestaw reguł domyślnych.</span><span class="sxs-lookup"><span data-stu-id="04064-177">All NSGs contain a set of default rules.</span></span> <span data-ttu-id="04064-178">Reguł domyślnych nie można usunąć, ale ponieważ mają przypisany najniższy priorytet, mogą być zastąpione przez tworzone zasady.</span><span class="sxs-lookup"><span data-stu-id="04064-178">The default rules cannot be deleted, but because they are assigned the lowest priority, they can be overridden by the rules that you create.</span></span>

- <span data-ttu-id="04064-179">**Sieć wirtualna** — ruch pochodzący i kończenie w sieci wirtualnej jest dozwolony zarówno w kierunkach przychodzących i wychodzących.</span><span class="sxs-lookup"><span data-stu-id="04064-179">**Virtual network** - Traffic originating and ending in a virtual network is allowed both in inbound and outbound directions.</span></span>
- <span data-ttu-id="04064-180">**Internet** — ruch wychodzący jest dozwolone, ale ruch przychodzący jest zablokowany.</span><span class="sxs-lookup"><span data-stu-id="04064-180">**Internet** - Outbound traffic is allowed, but inbound traffic is blocked.</span></span>
- <span data-ttu-id="04064-181">**Moduł równoważenia obciążenia** — umożliwia modułowi równoważenia obciążenia Azure badanie kondycji maszyn wirtualnych i wystąpień ról.</span><span class="sxs-lookup"><span data-stu-id="04064-181">**Load balancer** - Allow Azure’s load balancer to probe the health of your VMs and role instances.</span></span> <span data-ttu-id="04064-182">Tę zasadę można zastąpić, jeśli nie używasz zestawu o zrównoważonym obciążeniu.</span><span class="sxs-lookup"><span data-stu-id="04064-182">If you are not using a load balanced set, you can override this rule.</span></span>

### <a name="create-network-security-groups"></a><span data-ttu-id="04064-183">Utwórz grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="04064-183">Create network security groups</span></span>

<span data-ttu-id="04064-184">Można utworzyć grupy zabezpieczeń sieci w tym samym czasie jako maszynę Wirtualną przy użyciu [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="04064-184">A network security group can be created at the same time as a VM using the [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="04064-185">Gdy tak się grupa NSG jest skojarzona z interfejsu sieciowego maszyn wirtualnych i reguły NSG jest automatycznie utworzona zezwalająca na ruch na porcie *22* z dowolnego źródła.</span><span class="sxs-lookup"><span data-stu-id="04064-185">When doing so, the NSG is associated with the VMs network interface and an NSG rule is auto created to allow traffic on port *22* from any source.</span></span> <span data-ttu-id="04064-186">Wcześniej w tym samouczku frontonu NSG został automatycznie utworzony z maszyny Wirtualnej frontonu.</span><span class="sxs-lookup"><span data-stu-id="04064-186">Earlier in this tutorial, the front-end NSG was auto-created with the front-end VM.</span></span> <span data-ttu-id="04064-187">Reguły NSG również został automatycznie utworzony dla portu 22.</span><span class="sxs-lookup"><span data-stu-id="04064-187">An NSG rule was also auto created for port 22.</span></span> 

<span data-ttu-id="04064-188">W niektórych przypadkach może być przydatne do wstępnego tworzenia grupy NSG, takie jak kiedy nie należy tworzyć reguły domyślne SSH, lub gdy musi być podłączona grupa NSG do podsieci.</span><span class="sxs-lookup"><span data-stu-id="04064-188">In some cases, it may be helpful to pre-create an NSG, such as when default SSH rules should not be created, or when the NSG should be attached to a subnet.</span></span> 

<span data-ttu-id="04064-189">Użyj [utworzyć nsg sieci az](/cli/azure/network/nsg#create) polecenie, aby utworzyć grupę zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="04064-189">Use the [az network nsg create](/cli/azure/network/nsg#create) command to create a network security group.</span></span>

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

<span data-ttu-id="04064-190">Kojarzenie grupy NSG do interfejsu sieciowego, a nie jest skojarzony z podsiecią.</span><span class="sxs-lookup"><span data-stu-id="04064-190">Instead of associating the NSG to a network interface, it is associated with a subnet.</span></span> <span data-ttu-id="04064-191">W tej konfiguracji żadnej maszyny Wirtualnej, który jest podłączony do podsieci dziedziczy reguły NSG.</span><span class="sxs-lookup"><span data-stu-id="04064-191">In this configuration, any VM that is attached to the subnet inherits the NSG rules.</span></span>

<span data-ttu-id="04064-192">Aktualizuj istniejącą podsieć o nazwie *mySubnetBackEnd* z Nowa grupa NSG.</span><span class="sxs-lookup"><span data-stu-id="04064-192">Update the existing subnet named *mySubnetBackEnd* with the new NSG.</span></span>

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

<span data-ttu-id="04064-193">Teraz Utwórz maszynę wirtualną, która jest dołączona do *mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="04064-193">Now create a virtual machine, which is attached to the *mySubnetBackEnd*.</span></span> <span data-ttu-id="04064-194">Zwróć uwagę, że `--nsg` argument ma wartość pustą cudzysłowów.</span><span class="sxs-lookup"><span data-stu-id="04064-194">Notice that the `--nsg` argument has a value of empty double quotes.</span></span> <span data-ttu-id="04064-195">Grupy NSG nie muszą zostać utworzone z maszyną Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="04064-195">An NSG does not need to be created with the VM.</span></span> <span data-ttu-id="04064-196">Maszyna wirtualna jest podłączony do podsieci wewnętrznej, które są chronione za pomocą wstępnie utworzone NSG zaplecza.</span><span class="sxs-lookup"><span data-stu-id="04064-196">The VM is attached to the back-end subnet, which is protected with the pre-created back-end NSG.</span></span> <span data-ttu-id="04064-197">Ta grupa NSG stosuje się do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="04064-197">This NSG applies to the VM.</span></span> <span data-ttu-id="04064-198">Ponadto Zauważ, że `--public-ip-address` argument ma wartość pustą cudzysłowów.</span><span class="sxs-lookup"><span data-stu-id="04064-198">Also, notice here that the `--public-ip-address` argument has a value of empty double quotes.</span></span> <span data-ttu-id="04064-199">Ta konfiguracja tworzy Maszynę wirtualną bez publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="04064-199">This configuration creates a VM without a public IP address.</span></span> 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myBackEndVM \
  --vnet-name myVnet \
  --subnet mySubnetBackEnd \
  --public-ip-address "" \
  --nsg "" \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="secure-incoming-traffic"></a><span data-ttu-id="04064-200">Bezpieczny ruch przychodzący</span><span class="sxs-lookup"><span data-stu-id="04064-200">Secure incoming traffic</span></span>

<span data-ttu-id="04064-201">Podczas tworzenia maszyny Wirtualnej frontonu, reguły NSG utworzono zezwalająca na ruch przychodzący na porcie 22.</span><span class="sxs-lookup"><span data-stu-id="04064-201">When the front-end VM was created, an NSG rule was created to allow incoming traffic on port 22.</span></span> <span data-ttu-id="04064-202">Ta zasada umożliwia połączeń SSH z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="04064-202">This rule allows SSH connections to the VM.</span></span> <span data-ttu-id="04064-203">Na przykład ruch powinno być dozwolone na porcie *80*.</span><span class="sxs-lookup"><span data-stu-id="04064-203">For this example, traffic should also be allowed on port *80*.</span></span> <span data-ttu-id="04064-204">Ta konfiguracja pozwala na maszynie Wirtualnej dostęp do aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="04064-204">This configuration allows a web application to be accessed on the VM.</span></span>

<span data-ttu-id="04064-205">Użyj [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create) polecenie, aby utworzyć regułę dla portu *80*.</span><span class="sxs-lookup"><span data-stu-id="04064-205">Use the [az network nsg rule create](/cli/azure/network/nsg/rule#create) command to create a rule for port *80*.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGFrontEnd \
  --name http \
  --access allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range 80
```

<span data-ttu-id="04064-206">Frontonu maszyny Wirtualnej jest obecnie dostępny tylko na porcie *22* i port *80*.</span><span class="sxs-lookup"><span data-stu-id="04064-206">The front-end VM is now only accessible on port *22* and port *80*.</span></span> <span data-ttu-id="04064-207">Cały ruch przychodzący jest zablokowany na grupę zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="04064-207">All other incoming traffic is blocked at the network security group.</span></span> <span data-ttu-id="04064-208">Może to być przydatne do wizualizacji konfiguracjach reguły NSG.</span><span class="sxs-lookup"><span data-stu-id="04064-208">It may be helpful to visualize the NSG rule configurations.</span></span> <span data-ttu-id="04064-209">Zwraca konfigurację reguły NSG z [listy reguł sieciowej az](/cli/azure/network/nsg/rule#list) polecenia.</span><span class="sxs-lookup"><span data-stu-id="04064-209">Return the NSG rule configuration with the [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

<span data-ttu-id="04064-210">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="04064-210">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-to-vm-traffic"></a><span data-ttu-id="04064-211">Bezpiecznej maszyny Wirtualnej do ruchu maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="04064-211">Secure VM to VM traffic</span></span>

<span data-ttu-id="04064-212">Reguły grupy zabezpieczeń sieci można także zastosować między maszynami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="04064-212">Network security group rules can also apply between VMs.</span></span> <span data-ttu-id="04064-213">Na przykład frontonu maszyny Wirtualnej musi łączyć się z zaplecza maszyny Wirtualnej na porcie *22* i *3306*.</span><span class="sxs-lookup"><span data-stu-id="04064-213">For this example, the front-end VM needs to communicate with the back-end VM on port *22* and *3306*.</span></span> <span data-ttu-id="04064-214">Ta konfiguracja umożliwia połączeń SSH z frontonu maszyny Wirtualnej, a także zezwolić aplikacji na Maszynie wirtualnej frontonu do komunikowania się z wewnętrznej bazy danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="04064-214">This configuration allows SSH connections from the front-end VM, and also allow an application on the front-end VM to communicate with a back-end MySQL database.</span></span> <span data-ttu-id="04064-215">Powinien zostać zablokowany cały ruch między maszynami wirtualnymi frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="04064-215">All other traffic should be blocked between the front-end and back-end virtual machines.</span></span>

<span data-ttu-id="04064-216">Użyj [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create) polecenie, aby utworzyć regułę dla portu 22.</span><span class="sxs-lookup"><span data-stu-id="04064-216">Use the [az network nsg rule create](/cli/azure/network/nsg/rule#create) command to create a rule for port 22.</span></span> <span data-ttu-id="04064-217">Zwróć uwagę, że `--source-address-prefix` argument określa wartość *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="04064-217">Notice that the `--source-address-prefix` argument specifies a value of *10.0.1.0/24*.</span></span> <span data-ttu-id="04064-218">Taka konfiguracja powoduje, że za pośrednictwem grupa NSG jest dozwolone tylko na ruch z podsieci frontonu.</span><span class="sxs-lookup"><span data-stu-id="04064-218">This configuration ensures that only traffic from the front-end subnet is allowed through the NSG.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name SSH \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 100 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "22"
```

<span data-ttu-id="04064-219">Teraz Dodaj regułę dla ruchu danych MySQL na porcie 3306.</span><span class="sxs-lookup"><span data-stu-id="04064-219">Now add a rule for MySQL traffic on port 3306.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name MySQL \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "3306"
```

<span data-ttu-id="04064-220">Ponadto ponieważ grup NSG domyślną regułę zezwalającą na cały ruch między maszynami wirtualnymi w tej samej sieci wirtualnej, regułę można utworzyć dla grup NSG zaplecza zablokować cały ruch.</span><span class="sxs-lookup"><span data-stu-id="04064-220">Finally, because NSGs have a default rule allowing all traffic between VMs in the same VNet, a rule can be created for the back-end NSGs to block all traffic.</span></span> <span data-ttu-id="04064-221">Zauważ, że `--priority` znajduje się wartość *300*, która jest niższy tej reguły NSG i MySQL.</span><span class="sxs-lookup"><span data-stu-id="04064-221">Notice here that the `--priority` is given a value of *300*, which is lower that both the NSG and MySQL rules.</span></span> <span data-ttu-id="04064-222">Taka konfiguracja powoduje, że ruch SSH i MySQL nadal uzyskuje zezwolenie za pośrednictwem grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="04064-222">This configuration ensures that SSH and MySQL traffic is still allowed through the NSG.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name denyAll \
  --access Deny \
  --protocol Tcp \
  --direction Inbound \
  --priority 300 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "*"
```

<span data-ttu-id="04064-223">Maszyna wirtualna zaplecza jest teraz dostępny tylko na porcie *22* i port *3306* z podsieci frontonu.</span><span class="sxs-lookup"><span data-stu-id="04064-223">The back-end VM is now only accessible on port *22* and port *3306* from the front-end subnet.</span></span> <span data-ttu-id="04064-224">Cały ruch przychodzący jest zablokowany na grupę zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="04064-224">All other incoming traffic is blocked at the network security group.</span></span> <span data-ttu-id="04064-225">Może to być przydatne do wizualizacji konfiguracjach reguły NSG.</span><span class="sxs-lookup"><span data-stu-id="04064-225">It may be helpful to visualize the NSG rule configurations.</span></span> <span data-ttu-id="04064-226">Zwraca konfigurację reguły NSG z [listy reguł sieciowej az](/cli/azure/network/nsg/rule#list) polecenia.</span><span class="sxs-lookup"><span data-stu-id="04064-226">Return the NSG rule configuration with the [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

<span data-ttu-id="04064-227">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="04064-227">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a><span data-ttu-id="04064-228">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="04064-228">Next steps</span></span>

<span data-ttu-id="04064-229">W tym samouczku zostało utworzone i zabezpieczonej sieci platformy Azure w odniesieniu do maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="04064-229">In this tutorial, you created and secured Azure networks as related to virtual machines.</span></span> <span data-ttu-id="04064-230">Możesz przedstawiono sposób do:</span><span class="sxs-lookup"><span data-stu-id="04064-230">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="04064-231">Wdrażanie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="04064-231">Deploy a virtual network</span></span>
> * <span data-ttu-id="04064-232">Utwórz podsieć sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="04064-232">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="04064-233">Dołącz do podsieci maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="04064-233">Attach virtual machines to a subnet</span></span>
> * <span data-ttu-id="04064-234">Zarządzanie publicznych adresów IP maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="04064-234">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="04064-235">Bezpieczny ruch przychodzący z Internetu</span><span class="sxs-lookup"><span data-stu-id="04064-235">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="04064-236">Bezpiecznej maszyny Wirtualnej do ruchu maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="04064-236">Secure VM to VM traffic</span></span>

<span data-ttu-id="04064-237">Przejdź do następnego samouczka, aby dowiedzieć się więcej na temat zabezpieczania danych w przypadku maszyn wirtualnych przy użyciu kopii zapasowej systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="04064-237">Advance to the next tutorial to learn about securing data on virtual machines using Azure backup.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="04064-238">Tworzenie kopii zapasowych maszyn wirtualnych systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="04064-238">Back up Linux virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
