---
title: aaaAzure sieci wirtualnych i maszyn wirtualnych systemu Linux | Dokumentacja firmy Microsoft
description: "Samouczek — Zarządzanie sieciami wirtualnymi Azure i maszyn wirtualnych systemu Linux z hello Azure CLI"
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
ms.openlocfilehash: 57e6bd4de16f0e31d53dc67bf50dc5730d43712b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-hello-azure-cli"></a><span data-ttu-id="14be7-103">Zarządzanie sieciami wirtualnymi Azure i maszyn wirtualnych systemu Linux z hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="14be7-103">Manage Azure Virtual Networks and Linux Virtual Machines with hello Azure CLI</span></span>

<span data-ttu-id="14be7-104">Maszyny wirtualne platformy Azure używania sieci platformy Azure do komunikacji sieciowej wewnętrznych i zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="14be7-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="14be7-105">Ten samouczek przeprowadzi Cię przez wdrożenie dwóch maszyn wirtualnych i konfigurowanie sieci platformy Azure dla tych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="14be7-105">This tutorial walks through deploying two virtual machines and configuring Azure networking for these VMs.</span></span> <span data-ttu-id="14be7-106">Przykłady Hello w tym samouczku założono hello maszyny wirtualne obsługujące aplikacji sieci web z bazy danych zaplecza, jednak aplikacja nie zostanie wdrożona w samouczku hello.</span><span class="sxs-lookup"><span data-stu-id="14be7-106">hello examples in this tutorial assume that hello VMs are hosting a web application with a database back-end, however an application is not deployed in hello tutorial.</span></span> <span data-ttu-id="14be7-107">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="14be7-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="14be7-108">Wdrażanie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="14be7-108">Deploy a virtual network</span></span>
> * <span data-ttu-id="14be7-109">Utwórz podsieć sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="14be7-109">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="14be7-110">Dołącz podsieci tooa maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="14be7-110">Attach virtual machines tooa subnet</span></span>
> * <span data-ttu-id="14be7-111">Zarządzanie publicznych adresów IP maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="14be7-111">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="14be7-112">Bezpieczny ruch przychodzący z Internetu</span><span class="sxs-lookup"><span data-stu-id="14be7-112">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="14be7-113">Bezpieczny ruch tooVM maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="14be7-113">Secure VM tooVM traffic</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="14be7-114">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="14be7-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="14be7-115">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="14be7-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="14be7-116">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="14be7-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="vm-networking-overview"></a><span data-ttu-id="14be7-117">Omówienie sieci maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="14be7-117">VM networking overview</span></span>

<span data-ttu-id="14be7-118">Sieci wirtualnych platformy Azure włączyć bezpiecznych połączeń sieci między maszynami wirtualnymi, hello internet i innymi usługami Azure, takich jak bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="14be7-118">Azure virtual networks enable secure network connections between virtual machines, hello internet, and other Azure services such as Azure SQL database.</span></span> <span data-ttu-id="14be7-119">Sieci wirtualne są podzielone na segmentach logicznej podsieci.</span><span class="sxs-lookup"><span data-stu-id="14be7-119">Virtual networks are broken down into logical segments called subnets.</span></span> <span data-ttu-id="14be7-120">Podsieci są używane toocontrol przepływ sieci i funkcję granicy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="14be7-120">Subnets are used toocontrol network flow, and as a security boundary.</span></span> <span data-ttu-id="14be7-121">Podczas wdrażania maszyny Wirtualnej, zwykle obejmuje interfejs sieci wirtualnej, która jest dołączona tooa podsieci.</span><span class="sxs-lookup"><span data-stu-id="14be7-121">When deploying a VM, it generally includes a virtual network interface, which is attached tooa subnet.</span></span>

## <a name="deploy-virtual-network"></a><span data-ttu-id="14be7-122">Wdrażanie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="14be7-122">Deploy virtual network</span></span>

<span data-ttu-id="14be7-123">W tym samouczku jednej sieci wirtualnej jest tworzony z dwoma podsieciami.</span><span class="sxs-lookup"><span data-stu-id="14be7-123">For this tutorial, a single virtual network is created with two subnets.</span></span> <span data-ttu-id="14be7-124">Podsieci frontonu do obsługi aplikacji sieci web, a podsieć zaplecza dla hostingu serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="14be7-124">A front-end subnet for hosting a web application, and a back-end subnet for hosting a database server.</span></span>

<span data-ttu-id="14be7-125">Przed utworzeniem sieci wirtualnej, Utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="14be7-125">Before you can create a virtual network, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="14be7-126">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myRGNetwork* w lokalizacji eastus hello.</span><span class="sxs-lookup"><span data-stu-id="14be7-126">hello following example creates a resource group named *myRGNetwork* in hello eastus location.</span></span>

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a><span data-ttu-id="14be7-127">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="14be7-127">Create virtual network</span></span>

<span data-ttu-id="14be7-128">Witaj nam [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create) toocreate polecenia sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="14be7-128">Us hello [az network vnet create](/cli/azure/network/vnet#create) command toocreate a virtual network.</span></span> <span data-ttu-id="14be7-129">W tym przykładzie nosi nazwę sieci hello *mvVnet* i podano prefiksu adresu *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="14be7-129">In this example, hello network is named *mvVnet* and is given an address prefix of *10.0.0.0/16*.</span></span> <span data-ttu-id="14be7-130">Tworzona jest również podsieć o nazwie *mySubnetFrontEnd* i prefiksem *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="14be7-130">A subnet is also created with a name of *mySubnetFrontEnd* and a prefix of *10.0.1.0/24*.</span></span> <span data-ttu-id="14be7-131">W dalszej części tego samouczka frontonu maszyny Wirtualnej jest połączonych toothis podsieci.</span><span class="sxs-lookup"><span data-stu-id="14be7-131">Later in this tutorial a front-end VM is connected toothis subnet.</span></span> 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a><span data-ttu-id="14be7-132">Utwórz podsieć</span><span class="sxs-lookup"><span data-stu-id="14be7-132">Create subnet</span></span>

<span data-ttu-id="14be7-133">Nowa podsieć jest dodawany toohello sieci wirtualnej przy użyciu hello [Utwórz podsieć sieci wirtualnej sieci az](/cli/azure/network/vnet/subnet#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="14be7-133">A new subnet is added toohello virtual network using hello [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command.</span></span> <span data-ttu-id="14be7-134">W tym przykładzie hello podsieci o nazwie *mySubnetBackEnd* i podano prefiksu adresu *10.0.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="14be7-134">In this example, hello subnet is named *mySubnetBackEnd* and is given an address prefix of *10.0.2.0/24*.</span></span> <span data-ttu-id="14be7-135">Ta podsieć jest używany ze wszystkimi usługami zaplecza.</span><span class="sxs-lookup"><span data-stu-id="14be7-135">This subnet is used with all back-end services.</span></span>

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

<span data-ttu-id="14be7-136">W tym momencie sieci zostało utworzone i podzielone na dwie podsieci, jeden dla usługi frontonu i drugi dla usług zaplecza.</span><span class="sxs-lookup"><span data-stu-id="14be7-136">At this point, a network has been created and segmented into two subnets, one for front-end services, and another for back-end services.</span></span> <span data-ttu-id="14be7-137">W następnej sekcji hello maszyny wirtualne są tworzone i połączone toothese podsieci.</span><span class="sxs-lookup"><span data-stu-id="14be7-137">In hello next section, virtual machines are created and connected toothese subnets.</span></span>

## <a name="understand-public-ip-address"></a><span data-ttu-id="14be7-138">Zrozumienie publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="14be7-138">Understand public IP address</span></span>

<span data-ttu-id="14be7-139">Publiczny adres IP umożliwia toobe zasobów platformy Azure dostępna w hello internet.</span><span class="sxs-lookup"><span data-stu-id="14be7-139">A public IP address allows Azure resources toobe accessible on hello internet.</span></span> <span data-ttu-id="14be7-140">W tej sekcji samouczka hello maszyny Wirtualnej jest tworzony toodemonstrate jak adresy toowork z publicznym adresem IP.</span><span class="sxs-lookup"><span data-stu-id="14be7-140">In this section of hello tutorial, a VM is created toodemonstrate how toowork with public IP addresses.</span></span>

### <a name="allocation-method"></a><span data-ttu-id="14be7-141">Metoda alokacji</span><span class="sxs-lookup"><span data-stu-id="14be7-141">Allocation method</span></span>

<span data-ttu-id="14be7-142">Publiczny adres IP można przypisać jako dynamicznej lub statycznej.</span><span class="sxs-lookup"><span data-stu-id="14be7-142">A public IP address can be allocated as either dynamic or static.</span></span> <span data-ttu-id="14be7-143">Domyślnie dynamicznie przydzielane publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="14be7-143">By default, public IP address dynamically allocated.</span></span> <span data-ttu-id="14be7-144">Dynamiczne adresy IP są wydawane po cofnięciu przydziału maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="14be7-144">Dynamic IP addresses are released when a VM is deallocated.</span></span> <span data-ttu-id="14be7-145">To działanie powoduje toochange adres IP hello podczas żadnej operacji, która obejmuje dezalokacji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="14be7-145">This behavior causes hello IP address toochange during any operation that includes a VM deallocation.</span></span>

<span data-ttu-id="14be7-146">Metoda alokacji Hello można ustawić toostatic, który zapewnia pozostawienie hello adres IP przypisany tooa maszyny Wirtualnej, nawet podczas deallocated stanu.</span><span class="sxs-lookup"><span data-stu-id="14be7-146">hello allocation method can be set toostatic, which ensures that hello IP address remain assigned tooa VM, even during a deallocated state.</span></span> <span data-ttu-id="14be7-147">Korzystając z statycznie przydzielony adres IP, nie można określić sam adres IP hello.</span><span class="sxs-lookup"><span data-stu-id="14be7-147">When using a statically allocated IP address, hello IP address itself cannot be specified.</span></span> <span data-ttu-id="14be7-148">Zamiast tego jest ona przydzielone z puli dostępnych adresów.</span><span class="sxs-lookup"><span data-stu-id="14be7-148">Instead, it is allocated from a pool of available addresses.</span></span>

### <a name="dynamic-allocation"></a><span data-ttu-id="14be7-149">Dynamiczna alokacja</span><span class="sxs-lookup"><span data-stu-id="14be7-149">Dynamic allocation</span></span>

<span data-ttu-id="14be7-150">Podczas tworzenia maszyny Wirtualnej przy użyciu hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia hello domyślnego publicznego metoda adresu IP alokacji jest dynamiczny.</span><span class="sxs-lookup"><span data-stu-id="14be7-150">When creating a VM with hello [az vm create](/cli/azure/vm#create) command, hello default public IP address allocation method is dynamic.</span></span> <span data-ttu-id="14be7-151">W hello poniższy przykład maszyna wirtualna zostanie utworzona z dynamicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="14be7-151">In hello following example, a VM is created with a dynamic IP address.</span></span> 

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

### <a name="static-allocation"></a><span data-ttu-id="14be7-152">Statycznych alokacji</span><span class="sxs-lookup"><span data-stu-id="14be7-152">Static allocation</span></span>

<span data-ttu-id="14be7-153">Podczas tworzenia maszyny wirtualnej z wykorzystaniem hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia, obejmują hello `--public-ip-address-allocation static` tooassign argumentu statycznego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="14be7-153">When creating a virtual machine using hello [az vm create](/cli/azure/vm#create) command, include hello `--public-ip-address-allocation static` argument tooassign a static public IP address.</span></span> <span data-ttu-id="14be7-154">Ta operacja nie jest prezentowana w tym samouczku, jednak w następnej sekcji hello dynamicznie przydzielonego adresu IP jest zmienione tooa statycznie przydzielony adres.</span><span class="sxs-lookup"><span data-stu-id="14be7-154">This operation is not demonstrated in this tutorial, however in hello next section a dynamically allocated IP address is changed tooa statically allocated address.</span></span> 

### <a name="change-allocation-method"></a><span data-ttu-id="14be7-155">Zmień metodę alokacji</span><span class="sxs-lookup"><span data-stu-id="14be7-155">Change allocation method</span></span>

<span data-ttu-id="14be7-156">Metoda alokacji adresu IP Hello można zmienić za pomocą hello [az sieci ip publicznego aktualizacji](/cli/azure/network/public-ip#update) polecenia.</span><span class="sxs-lookup"><span data-stu-id="14be7-156">hello IP address allocation method can be changed using hello [az network public-ip update](/cli/azure/network/public-ip#update) command.</span></span> <span data-ttu-id="14be7-157">W tym przykładzie hello metoda alokacji adresów IP hello frontonu maszyny Wirtualnej zostanie zmieniona toostatic.</span><span class="sxs-lookup"><span data-stu-id="14be7-157">In this example, hello IP address allocation method of hello front-end VM is changed toostatic.</span></span>

<span data-ttu-id="14be7-158">Najpierw cofnąć hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="14be7-158">First, deallocate hello VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

<span data-ttu-id="14be7-159">Użyj hello [az sieci ip publicznego aktualizacji](/cli/azure/network/public-ip#update) metodę alokacji hello tooupdate polecenia.</span><span class="sxs-lookup"><span data-stu-id="14be7-159">Use hello [az network public-ip update](/cli/azure/network/public-ip#update) command tooupdate hello allocation method.</span></span> <span data-ttu-id="14be7-160">W takim przypadku hello `--allocation-method` jest ustawiany za*statycznych*.</span><span class="sxs-lookup"><span data-stu-id="14be7-160">In this case, hello `--allocation-method` is being set too*static*.</span></span>

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

<span data-ttu-id="14be7-161">Uruchom hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="14be7-161">Start hello VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a><span data-ttu-id="14be7-162">Nie publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="14be7-162">No public IP address</span></span>

<span data-ttu-id="14be7-163">Często maszyny Wirtualnej nie jest konieczne toobe dostępna przez hello internet.</span><span class="sxs-lookup"><span data-stu-id="14be7-163">Often, a VM does not need toobe accessible over hello internet.</span></span> <span data-ttu-id="14be7-164">toocreate Maszynę wirtualną bez publicznego adresu IP, użyj hello `--public-ip-address ""` argumentu z pustego zestawu cudzysłowów.</span><span class="sxs-lookup"><span data-stu-id="14be7-164">toocreate a VM without a public IP address, use hello `--public-ip-address ""` argument with an empty set of double quotes.</span></span> <span data-ttu-id="14be7-165">Ta konfiguracja jest przedstawiona w dalszej części tego samouczka</span><span class="sxs-lookup"><span data-stu-id="14be7-165">This configuration is demonstrated later in this tutorial</span></span>

## <a name="secure-network-traffic"></a><span data-ttu-id="14be7-166">Zabezpieczanie ruchu sieciowego</span><span class="sxs-lookup"><span data-stu-id="14be7-166">Secure network traffic</span></span>

<span data-ttu-id="14be7-167">Grupa zabezpieczeń sieci (NSG) zawiera listę reguł zabezpieczeń, które Zezwalaj lub Odmów tooresources ruchu sieciowego połączone sieci wirtualne tooAzure (VNet).</span><span class="sxs-lookup"><span data-stu-id="14be7-167">A network security group (NSG) contains a list of security rules that allow or deny network traffic tooresources connected tooAzure Virtual Networks (VNet).</span></span> <span data-ttu-id="14be7-168">Grupy NSG mogą być skojarzone toosubnets lub do interfejsów sieciowych poszczególnych.</span><span class="sxs-lookup"><span data-stu-id="14be7-168">NSGs can be associated toosubnets or individual network interfaces.</span></span> <span data-ttu-id="14be7-169">Grupa NSG jest skojarzona z karty sieciowej, stosuje się tylko hello skojarzonego VM.</span><span class="sxs-lookup"><span data-stu-id="14be7-169">When an NSG is associated with a network interface, it applies only hello associated VM.</span></span> <span data-ttu-id="14be7-170">Gdy grupa NSG jest skojarzona tooa podsieci, mają zastosowanie reguły hello tooall zasobów połączonych toohello podsieci.</span><span class="sxs-lookup"><span data-stu-id="14be7-170">When an NSG is associated tooa subnet, hello rules apply tooall resources connected toohello subnet.</span></span> 

### <a name="network-security-group-rules"></a><span data-ttu-id="14be7-171">Reguły grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="14be7-171">Network security group rules</span></span>

<span data-ttu-id="14be7-172">Reguły NSG definiują portów sieciowych za pośrednictwem których ruch jest dozwolony lub niedozwolony.</span><span class="sxs-lookup"><span data-stu-id="14be7-172">NSG rules define networking ports over which traffic is allowed or denied.</span></span> <span data-ttu-id="14be7-173">reguły Hello mogą obejmować źródłowe i docelowe zakresów adresów IP tak, aby ruch jest kontrolowany między konkretnych systemów lub podsieci.</span><span class="sxs-lookup"><span data-stu-id="14be7-173">hello rules can include source and destination IP address ranges so that traffic is controlled between specific systems or subnets.</span></span> <span data-ttu-id="14be7-174">Reguły NSG obejmują także priorytet (od 1 — i 4096).</span><span class="sxs-lookup"><span data-stu-id="14be7-174">NSG rules also include a priority (between 1—and 4096).</span></span> <span data-ttu-id="14be7-175">Reguły są sprawdzane hello według priorytetu.</span><span class="sxs-lookup"><span data-stu-id="14be7-175">Rules are evaluated in hello order of priority.</span></span> <span data-ttu-id="14be7-176">Reguła o priorytecie 100 jest oceniane przed regułą z priorytetem 200.</span><span class="sxs-lookup"><span data-stu-id="14be7-176">A rule with a priority of 100 is evaluated before a rule with priority 200.</span></span>

<span data-ttu-id="14be7-177">Wszystkie sieciowe grupy zabezpieczeń zawierają zestaw reguł domyślnych.</span><span class="sxs-lookup"><span data-stu-id="14be7-177">All NSGs contain a set of default rules.</span></span> <span data-ttu-id="14be7-178">Nie można usunąć reguły domyślne Hello, ale ponieważ mają przypisany najniższy priorytet hello, mogą być zastąpione przez hello utworzonych reguł.</span><span class="sxs-lookup"><span data-stu-id="14be7-178">hello default rules cannot be deleted, but because they are assigned hello lowest priority, they can be overridden by hello rules that you create.</span></span>

- <span data-ttu-id="14be7-179">**Sieć wirtualna** — ruch pochodzący i kończenie w sieci wirtualnej jest dozwolony zarówno w kierunkach przychodzących i wychodzących.</span><span class="sxs-lookup"><span data-stu-id="14be7-179">**Virtual network** - Traffic originating and ending in a virtual network is allowed both in inbound and outbound directions.</span></span>
- <span data-ttu-id="14be7-180">**Internet** — ruch wychodzący jest dozwolone, ale ruch przychodzący jest zablokowany.</span><span class="sxs-lookup"><span data-stu-id="14be7-180">**Internet** - Outbound traffic is allowed, but inbound traffic is blocked.</span></span>
- <span data-ttu-id="14be7-181">**Moduł równoważenia obciążenia** — Zezwalaj Azure kondycji hello tooprobe usługi równoważenia obciążenia maszyn wirtualnych i wystąpień ról.</span><span class="sxs-lookup"><span data-stu-id="14be7-181">**Load balancer** - Allow Azure’s load balancer tooprobe hello health of your VMs and role instances.</span></span> <span data-ttu-id="14be7-182">Tę zasadę można zastąpić, jeśli nie używasz zestawu o zrównoważonym obciążeniu.</span><span class="sxs-lookup"><span data-stu-id="14be7-182">If you are not using a load balanced set, you can override this rule.</span></span>

### <a name="create-network-security-groups"></a><span data-ttu-id="14be7-183">Utwórz grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="14be7-183">Create network security groups</span></span>

<span data-ttu-id="14be7-184">Grupy zabezpieczeń sieci można tworzyć na powitania sam czasu jako Maszynę wirtualną przy użyciu hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="14be7-184">A network security group can be created at hello same time as a VM using hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="14be7-185">W takiej hello grupa NSG jest skojarzona z interfejsu sieciowego maszyn wirtualnych hello i reguły NSG jest automatycznie utworzona tooallow ruch na porcie *22* z dowolnego źródła.</span><span class="sxs-lookup"><span data-stu-id="14be7-185">When doing so, hello NSG is associated with hello VMs network interface and an NSG rule is auto created tooallow traffic on port *22* from any source.</span></span> <span data-ttu-id="14be7-186">Wcześniej w tym samouczku powitalne frontonu NSG został utworzony automatycznie z hello frontonu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="14be7-186">Earlier in this tutorial, hello front-end NSG was auto-created with hello front-end VM.</span></span> <span data-ttu-id="14be7-187">Reguły NSG również został automatycznie utworzony dla portu 22.</span><span class="sxs-lookup"><span data-stu-id="14be7-187">An NSG rule was also auto created for port 22.</span></span> 

<span data-ttu-id="14be7-188">W niektórych przypadkach może być przydatne toopre — Utwórz grupy NSG, takie jak kiedy nie należy tworzyć reguły domyślne SSH lub gdy hello NSG powinna być dołączone tooa podsieci.</span><span class="sxs-lookup"><span data-stu-id="14be7-188">In some cases, it may be helpful toopre-create an NSG, such as when default SSH rules should not be created, or when hello NSG should be attached tooa subnet.</span></span> 

<span data-ttu-id="14be7-189">Użyj hello [utworzyć nsg sieci az](/cli/azure/network/nsg#create) toocreate polecenia sieciowej grupy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="14be7-189">Use hello [az network nsg create](/cli/azure/network/nsg#create) command toocreate a network security group.</span></span>

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

<span data-ttu-id="14be7-190">Zamiast skojarzenie interfejsu sieciowego tooa NSG hello, jest skojarzona z podsiecią.</span><span class="sxs-lookup"><span data-stu-id="14be7-190">Instead of associating hello NSG tooa network interface, it is associated with a subnet.</span></span> <span data-ttu-id="14be7-191">W tej konfiguracji żadnej maszyny Wirtualnej, która jest dołączona toohello podsieci dziedziczy hello reguły NSG.</span><span class="sxs-lookup"><span data-stu-id="14be7-191">In this configuration, any VM that is attached toohello subnet inherits hello NSG rules.</span></span>

<span data-ttu-id="14be7-192">Aktualizuj istniejącą podsieć hello o nazwie *mySubnetBackEnd* z hello Nowa grupa NSG.</span><span class="sxs-lookup"><span data-stu-id="14be7-192">Update hello existing subnet named *mySubnetBackEnd* with hello new NSG.</span></span>

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

<span data-ttu-id="14be7-193">Teraz Utwórz maszynę wirtualną, która jest dołączona toohello *mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="14be7-193">Now create a virtual machine, which is attached toohello *mySubnetBackEnd*.</span></span> <span data-ttu-id="14be7-194">Zwróć uwagę, że hello `--nsg` argument ma wartość pustą cudzysłowów.</span><span class="sxs-lookup"><span data-stu-id="14be7-194">Notice that hello `--nsg` argument has a value of empty double quotes.</span></span> <span data-ttu-id="14be7-195">Grupy NSG toobe utworzone za pomocą hello maszyny Wirtualnej nie jest konieczne.</span><span class="sxs-lookup"><span data-stu-id="14be7-195">An NSG does not need toobe created with hello VM.</span></span> <span data-ttu-id="14be7-196">Hello maszyny Wirtualnej jest dołączone toohello zaplecza podsieci, które są chronione za pomocą hello wstępnie utworzone NSG zaplecza.</span><span class="sxs-lookup"><span data-stu-id="14be7-196">hello VM is attached toohello back-end subnet, which is protected with hello pre-created back-end NSG.</span></span> <span data-ttu-id="14be7-197">Ta grupa NSG stosowana toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="14be7-197">This NSG applies toohello VM.</span></span> <span data-ttu-id="14be7-198">Ponadto Zauważ, że hello `--public-ip-address` argument ma wartość pustą cudzysłowów.</span><span class="sxs-lookup"><span data-stu-id="14be7-198">Also, notice here that hello `--public-ip-address` argument has a value of empty double quotes.</span></span> <span data-ttu-id="14be7-199">Ta konfiguracja tworzy Maszynę wirtualną bez publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="14be7-199">This configuration creates a VM without a public IP address.</span></span> 

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

### <a name="secure-incoming-traffic"></a><span data-ttu-id="14be7-200">Bezpieczny ruch przychodzący</span><span class="sxs-lookup"><span data-stu-id="14be7-200">Secure incoming traffic</span></span>

<span data-ttu-id="14be7-201">Gdy hello frontonu maszyna wirtualna została utworzona, NSG utworzono regułę ruchu przychodzącego tooallow port 22.</span><span class="sxs-lookup"><span data-stu-id="14be7-201">When hello front-end VM was created, an NSG rule was created tooallow incoming traffic on port 22.</span></span> <span data-ttu-id="14be7-202">Ta zasada umożliwia toohello połączenia SSH maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="14be7-202">This rule allows SSH connections toohello VM.</span></span> <span data-ttu-id="14be7-203">Na przykład ruch powinno być dozwolone na porcie *80*.</span><span class="sxs-lookup"><span data-stu-id="14be7-203">For this example, traffic should also be allowed on port *80*.</span></span> <span data-ttu-id="14be7-204">Ta konfiguracja pozwala toobe aplikacji sieci web, dostępny na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="14be7-204">This configuration allows a web application toobe accessed on hello VM.</span></span>

<span data-ttu-id="14be7-205">Użyj hello [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create) toocreate polecenia reguły portu *80*.</span><span class="sxs-lookup"><span data-stu-id="14be7-205">Use hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command toocreate a rule for port *80*.</span></span>

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

<span data-ttu-id="14be7-206">Witaj frontonu maszyny Wirtualnej jest obecnie dostępny tylko na porcie *22* i port *80*.</span><span class="sxs-lookup"><span data-stu-id="14be7-206">hello front-end VM is now only accessible on port *22* and port *80*.</span></span> <span data-ttu-id="14be7-207">Cały ruch przychodzący jest zablokowany na powitania sieciowej grupy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="14be7-207">All other incoming traffic is blocked at hello network security group.</span></span> <span data-ttu-id="14be7-208">Może to być przydatne toovisualize hello NSG reguły konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="14be7-208">It may be helpful toovisualize hello NSG rule configurations.</span></span> <span data-ttu-id="14be7-209">Konfiguracja reguły NSG hello zwracany z hello [listy reguł sieciowej az](/cli/azure/network/nsg/rule#list) polecenia.</span><span class="sxs-lookup"><span data-stu-id="14be7-209">Return hello NSG rule configuration with hello [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

<span data-ttu-id="14be7-210">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="14be7-210">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-toovm-traffic"></a><span data-ttu-id="14be7-211">Bezpieczny ruch tooVM maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="14be7-211">Secure VM tooVM traffic</span></span>

<span data-ttu-id="14be7-212">Reguły grupy zabezpieczeń sieci można także zastosować między maszynami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="14be7-212">Network security group rules can also apply between VMs.</span></span> <span data-ttu-id="14be7-213">Na przykład hello frontonu maszyny Wirtualnej musi toocommunicate z hello wirtualna zaplecza na porcie *22* i *3306*.</span><span class="sxs-lookup"><span data-stu-id="14be7-213">For this example, hello front-end VM needs toocommunicate with hello back-end VM on port *22* and *3306*.</span></span> <span data-ttu-id="14be7-214">Taka konfiguracja pozwala połączeń SSH z hello frontonu maszyny Wirtualnej, a także zezwolić aplikacji na powitania frontonu toocommunicate maszyny Wirtualnej z wewnętrznej bazy danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="14be7-214">This configuration allows SSH connections from hello front-end VM, and also allow an application on hello front-end VM toocommunicate with a back-end MySQL database.</span></span> <span data-ttu-id="14be7-215">Powinien zostać zablokowany cały ruch między maszynami wirtualnymi hello frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="14be7-215">All other traffic should be blocked between hello front-end and back-end virtual machines.</span></span>

<span data-ttu-id="14be7-216">Użyj hello [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create) toocreate polecenia regułę port 22.</span><span class="sxs-lookup"><span data-stu-id="14be7-216">Use hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command toocreate a rule for port 22.</span></span> <span data-ttu-id="14be7-217">Zwróć uwagę, że hello `--source-address-prefix` argument określa wartość *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="14be7-217">Notice that hello `--source-address-prefix` argument specifies a value of *10.0.1.0/24*.</span></span> <span data-ttu-id="14be7-218">Taka konfiguracja powoduje, że tylko na ruch z podsieci frontonu hello jest dozwolone przez hello NSG.</span><span class="sxs-lookup"><span data-stu-id="14be7-218">This configuration ensures that only traffic from hello front-end subnet is allowed through hello NSG.</span></span>

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

<span data-ttu-id="14be7-219">Teraz Dodaj regułę dla ruchu danych MySQL na porcie 3306.</span><span class="sxs-lookup"><span data-stu-id="14be7-219">Now add a rule for MySQL traffic on port 3306.</span></span>

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

<span data-ttu-id="14be7-220">Na koniec, ponieważ stosowanie reguły domyślnej grupy NSG cały ruch między maszynami wirtualnymi w hello sam sieci wirtualnej, regułę można utworzyć hello zaplecza grup NSG tooblock cały ruch.</span><span class="sxs-lookup"><span data-stu-id="14be7-220">Finally, because NSGs have a default rule allowing all traffic between VMs in hello same VNet, a rule can be created for hello back-end NSGs tooblock all traffic.</span></span> <span data-ttu-id="14be7-221">Zauważ, że hello `--priority` znajduje się wartość *300*, która jest niższe, że oba hello reguły NSG i MySQL.</span><span class="sxs-lookup"><span data-stu-id="14be7-221">Notice here that hello `--priority` is given a value of *300*, which is lower that both hello NSG and MySQL rules.</span></span> <span data-ttu-id="14be7-222">Taka konfiguracja powoduje, że ruchu SSH i MySQL nadal uzyskuje zezwolenie za pośrednictwem hello NSG.</span><span class="sxs-lookup"><span data-stu-id="14be7-222">This configuration ensures that SSH and MySQL traffic is still allowed through hello NSG.</span></span>

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

<span data-ttu-id="14be7-223">Witaj zaplecza maszyna wirtualna jest teraz dostępny tylko na porcie *22* i port *3306* z podsieci frontonu hello.</span><span class="sxs-lookup"><span data-stu-id="14be7-223">hello back-end VM is now only accessible on port *22* and port *3306* from hello front-end subnet.</span></span> <span data-ttu-id="14be7-224">Cały ruch przychodzący jest zablokowany na powitania sieciowej grupy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="14be7-224">All other incoming traffic is blocked at hello network security group.</span></span> <span data-ttu-id="14be7-225">Może to być przydatne toovisualize hello NSG reguły konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="14be7-225">It may be helpful toovisualize hello NSG rule configurations.</span></span> <span data-ttu-id="14be7-226">Konfiguracja reguły NSG hello zwracany z hello [listy reguł sieciowej az](/cli/azure/network/nsg/rule#list) polecenia.</span><span class="sxs-lookup"><span data-stu-id="14be7-226">Return hello NSG rule configuration with hello [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

<span data-ttu-id="14be7-227">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="14be7-227">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a><span data-ttu-id="14be7-228">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="14be7-228">Next steps</span></span>

<span data-ttu-id="14be7-229">W tym samouczku zostało utworzone i zabezpieczonej sieci platformy Azure jako powiązane toovirtual maszyny.</span><span class="sxs-lookup"><span data-stu-id="14be7-229">In this tutorial, you created and secured Azure networks as related toovirtual machines.</span></span> <span data-ttu-id="14be7-230">W tym samouczku omówiono:</span><span class="sxs-lookup"><span data-stu-id="14be7-230">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="14be7-231">Wdrażanie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="14be7-231">Deploy a virtual network</span></span>
> * <span data-ttu-id="14be7-232">Utwórz podsieć sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="14be7-232">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="14be7-233">Dołącz podsieci tooa maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="14be7-233">Attach virtual machines tooa subnet</span></span>
> * <span data-ttu-id="14be7-234">Zarządzanie publicznych adresów IP maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="14be7-234">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="14be7-235">Bezpieczny ruch przychodzący z Internetu</span><span class="sxs-lookup"><span data-stu-id="14be7-235">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="14be7-236">Bezpieczny ruch tooVM maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="14be7-236">Secure VM tooVM traffic</span></span>

<span data-ttu-id="14be7-237">Przejdź dalej toolearn samouczka toohello Zabezpieczanie danych w przypadku maszyn wirtualnych przy użyciu kopii zapasowej systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="14be7-237">Advance toohello next tutorial toolearn about securing data on virtual machines using Azure backup.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="14be7-238">Tworzenie kopii zapasowych maszyn wirtualnych systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="14be7-238">Back up Linux virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
