---
title: "Samouczek — kompilacji wysoką dostępność aplikacji na maszynach wirtualnych Azure | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie tworzenia aplikacji wysokiej dostępności i bezpieczne w trzech maszyn wirtualnych systemu Windows z usługą równoważenia obciążenia na platformie Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 03/30/2017
ms.author: davidmu
ms.openlocfilehash: 4b8690a11ec0e711782a112622e1193c24292289
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a><span data-ttu-id="60e0f-103">Tworzenie równoważone, wysoką dostępność aplikacji na maszynach wirtualnych systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="60e0f-103">Build a load balanced, highly available application on Windows virtual machines in Azure</span></span>

<span data-ttu-id="60e0f-104">W tym samouczku utworzysz wysokiej dostępności aplikacji, która jest odporność obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="60e0f-104">In this tutorial, you create a highly available application that is resilient to maintenance events.</span></span> <span data-ttu-id="60e0f-105">Aplikacja korzysta z modułu równoważenia obciążenia, zestawu dostępności i trzech maszyn wirtualnych systemu Windows (VM).</span><span class="sxs-lookup"><span data-stu-id="60e0f-105">The app uses a load balancer, an availability set, and three Windows virtual machines (VMs).</span></span> <span data-ttu-id="60e0f-106">W tym samouczku instaluje usługi IIS, chociaż można użyć w tym samouczku framework innej aplikacji, przy użyciu tego samego składniki wysokiej dostępności i wskazówki dotyczące wdrażania.</span><span class="sxs-lookup"><span data-stu-id="60e0f-106">This tutorial installs IIS, though you can use this tutorial to deploy a different application framework using the same high availability components and guidelines.</span></span> 

## <a name="step-1---azure-prerequisites"></a><span data-ttu-id="60e0f-107">Krok 1 — wymagania wstępne platformy Azure</span><span class="sxs-lookup"><span data-stu-id="60e0f-107">Step 1 - Azure prerequisites</span></span>

<span data-ttu-id="60e0f-108">Do ukończenia tego samouczka, upewnij się, że zainstalowano najnowszą [programu Azure PowerShell](/powershell/azure/overview) modułu.</span><span class="sxs-lookup"><span data-stu-id="60e0f-108">To complete this tutorial, make sure that you have installed the latest [Azure PowerShell](/powershell/azure/overview) module.</span></span>

<span data-ttu-id="60e0f-109">Najpierw należy zalogować się do Twojej subskrypcji platformy Azure przy użyciu polecenia Login-AzureRmAccount i postępuj zgodnie z wyświetlanymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="60e0f-109">First, log in to your Azure subscription with the Login-AzureRmAccount command and follow the on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="60e0f-110">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="60e0f-110">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="60e0f-111">Przed utworzeniem innych zasobów platformy Azure, musisz utworzyć nową grupę zasobów o [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="60e0f-111">Before you can create any other Azure resources, you need to create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="60e0f-112">Poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w `westeurope` regionu:</span><span class="sxs-lookup"><span data-stu-id="60e0f-112">The following example creates a resource group named `myResourceGroup` in the `westeurope` region:</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a><span data-ttu-id="60e0f-113">Krok 2 — Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="60e0f-113">Step 2 - Create availability set</span></span>

<span data-ttu-id="60e0f-114">Maszyny wirtualne mogą być tworzone przez błędów logicznych i Aktualizacja domeny.</span><span class="sxs-lookup"><span data-stu-id="60e0f-114">Virtual machines can be created across logical fault and update domains.</span></span> <span data-ttu-id="60e0f-115">Każdej domeny logicznej reprezentuje część sprzętu w podstawowej centrum danych Azure.</span><span class="sxs-lookup"><span data-stu-id="60e0f-115">Each logical domain represents a portion of hardware in the underlying Azure datacenter.</span></span> <span data-ttu-id="60e0f-116">Po utworzeniu co najmniej dwie maszyny wirtualne, zasobów obliczeniowych i przestrzeni dyskowej są dystrybuowane w tych domenach.</span><span class="sxs-lookup"><span data-stu-id="60e0f-116">When you create two or more VMs, your compute and storage resources are distributed across these domains.</span></span> <span data-ttu-id="60e0f-117">Tej dystrybucji przechowuje dostępność aplikacji, jeśli składnik sprzętowy wymaga konserwacji.</span><span class="sxs-lookup"><span data-stu-id="60e0f-117">This distribution maintains the availability of your app if a hardware component needs maintenance.</span></span> <span data-ttu-id="60e0f-118">Zestawy dostępności umożliwiają zdefiniowanie tych logicznej domen błędów i aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="60e0f-118">Availability sets let you define these logical fault and update domains.</span></span>

<span data-ttu-id="60e0f-119">Utwórz zestaw o dostępności [AzureRmAvailabilitySet nowy](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="60e0f-119">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="60e0f-120">Poniższy przykład tworzy zbiór nazwanego dostępności `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="60e0f-120">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a><span data-ttu-id="60e0f-121">Krok 3 — Tworzenie obciążenia równoważenia</span><span class="sxs-lookup"><span data-stu-id="60e0f-121">Step 3 - Create load balancer</span></span>

<span data-ttu-id="60e0f-122">Moduł równoważenia obciążenia Azure dystrybuuje ruch zestawu zdefiniowanego maszyn wirtualnych przy użyciu reguły modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="60e0f-122">An Azure load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="60e0f-123">Badania kondycji monitoruje danego portu na każdej maszynie Wirtualnej i tylko dystrybuuje ruch do operacyjnej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="60e0f-123">A health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span>

### <a name="create-public-ip-address"></a><span data-ttu-id="60e0f-124">Utwórz publiczny adres IP</span><span class="sxs-lookup"><span data-stu-id="60e0f-124">Create public IP address</span></span>

<span data-ttu-id="60e0f-125">Aby uzyskać dostęp do aplikacji w Internecie, należy przypisać publicznego adresu IP usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="60e0f-125">To access your app on the Internet, assign a public IP address to the load balancer.</span></span> <span data-ttu-id="60e0f-126">Utwórz publiczny adres IP z [AzureRmPublicIpAddress nowy](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="60e0f-126">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="60e0f-127">Poniższy przykład tworzy publiczny adres IP o nazwie `myPublicIP`:</span><span class="sxs-lookup"><span data-stu-id="60e0f-127">The following example creates a public IP address named `myPublicIP`:</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a><span data-ttu-id="60e0f-128">Tworzenie usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="60e0f-128">Create load balancer</span></span>

<span data-ttu-id="60e0f-129">Utwórz na adres IP frontonu [AzureRmLoadBalancerFrontendIpConfig nowy](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="60e0f-129">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="60e0f-130">Poniższy przykład tworzy adresu IP serwera sieci Web o nazwie `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="60e0f-130">The following example creates a frontend IP address named `myFrontEndPool`:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

<span data-ttu-id="60e0f-131">Utwórz pulę adresów zaplecza z [AzureRmLoadBalancerBackendAddressPoolConfig nowy](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="60e0f-131">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="60e0f-132">Poniższy przykład tworzy puli adresów zaplecza, o nazwie `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="60e0f-132">The following example creates a backend address pool named `myBackEndPool`:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="60e0f-133">Teraz Utwórz moduł równoważenia obciążenia z [AzureRmLoadBalancer nowy](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="60e0f-133">Now, create the load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="60e0f-134">Poniższy przykład tworzy moduł równoważenia obciążenia o nazwie `myLoadBalancer` przy użyciu `myPublicIP` adres:</span><span class="sxs-lookup"><span data-stu-id="60e0f-134">The following example creates a load balancer named `myLoadBalancer` using the `myPublicIP` address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a><span data-ttu-id="60e0f-135">Utworzyć sondy kondycji</span><span class="sxs-lookup"><span data-stu-id="60e0f-135">Create health probe</span></span>

<span data-ttu-id="60e0f-136">Aby zezwolić usłudze równoważenia obciążenia do monitorowania stanu aplikacji, należy użyć sondy kondycji.</span><span class="sxs-lookup"><span data-stu-id="60e0f-136">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="60e0f-137">Sondy kondycji dynamicznie dodaje lub usuwa maszyn wirtualnych z oparte na ich odpowiedzi na sprawdzenie kondycji obrót usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="60e0f-137">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="60e0f-138">Domyślnie maszyny Wirtualnej zostanie usunięte z dystrybucji modułu równoważenia obciążenia po dwóch kolejnych błędów na 15 sekund.</span><span class="sxs-lookup"><span data-stu-id="60e0f-138">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span></span>

<span data-ttu-id="60e0f-139">Utwórz badanie kondycji z [AzureRmLoadBalancerProbeConfig Dodaj](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="60e0f-139">Create a health probe with [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="60e0f-140">Poniższy przykład tworzy badanie kondycji o nazwie `myHealthProbe` który monitoruje każdej maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="60e0f-140">The following example creates a health probe named `myHealthProbe` that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a><span data-ttu-id="60e0f-141">Tworzenie reguły modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="60e0f-141">Create load balancer rule</span></span>

<span data-ttu-id="60e0f-142">Reguły modułu równoważenia obciążenia jest używany do definiowania rozkład ruchu do maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="60e0f-142">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span>

<span data-ttu-id="60e0f-143">Tworzenie reguły modułu równoważenia obciążenia z [AzureRmLoadBalancerRuleConfig Dodaj](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="60e0f-143">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="60e0f-144">Poniższy przykład tworzy regułę równoważenia obciążenia o nazwie `myLoadBalancerRule` i równoważy ruch na porcie `80`:</span><span class="sxs-lookup"><span data-stu-id="60e0f-144">The following example creates a load balancer rule named `myLoadBalancerRule` and balances traffic on port `80`:</span></span>

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

<span data-ttu-id="60e0f-145">Aktualizacja usługi równoważenia obciążenia z [AzureRmLoadBalancer zestaw](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="60e0f-145">Update the load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a><span data-ttu-id="60e0f-146">Krok 4 — Konfigurowanie sieci</span><span class="sxs-lookup"><span data-stu-id="60e0f-146">Step 4 - Configure networking</span></span>

<span data-ttu-id="60e0f-147">Każda maszyna wirtualna ma co najmniej jeden wirtualny kart interfejsu sieciowego (NIC) łączących się z siecią wirtualną.</span><span class="sxs-lookup"><span data-stu-id="60e0f-147">Each VM has one or more virtual network interface cards (NICs) that connect to a virtual network.</span></span> <span data-ttu-id="60e0f-148">Ta sieć wirtualna jest chroniona do filtrowania ruchu na podstawie reguł zdefiniowanych dostępu.</span><span class="sxs-lookup"><span data-stu-id="60e0f-148">This virtual network is secured to filter traffic based on defined access rules.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="60e0f-149">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="60e0f-149">Create virtual network</span></span>

<span data-ttu-id="60e0f-150">Skonfiguruj podsieci z [AzureRmVirtualNetworkSubnetConfig nowy](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="60e0f-150">First, configure a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="60e0f-151">Poniższy przykład tworzy podsieć o nazwie `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="60e0f-151">The following example creates a subnet named `mySubnet`:</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="60e0f-152">Aby zapewnić łączność sieciową dla maszyn wirtualnych, Utwórz sieć wirtualną z [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="60e0f-152">To provide network connectivity to your VMs, create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="60e0f-153">Poniższy przykład tworzy sieć wirtualną o nazwie `myVnet` z `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="60e0f-153">The following example creates a virtual network named `myVnet` with `mySubnet`:</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a><span data-ttu-id="60e0f-154">Konfigurowanie zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="60e0f-154">Configure network security</span></span>

<span data-ttu-id="60e0f-155">Azure [sieciowej grupy zabezpieczeń](../../virtual-network/virtual-networks-nsg.md) (NSG) steruje ruchu przychodzącego i wychodzącego dla jednego lub wielu maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="60e0f-155">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="60e0f-156">Reguły grupy zabezpieczeń sieci akceptować lub odrzucać ruchu sieciowego na określonym porcie lub zakres portów.</span><span class="sxs-lookup"><span data-stu-id="60e0f-156">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="60e0f-157">Te zasady mogą również obejmować prefiks adresu źródłowego, dzięki czemu tylko ruch w źródle wstępnie zdefiniowanych może komunikować się z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="60e0f-157">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span>

<span data-ttu-id="60e0f-158">Aby zezwolić na ruch w sieci web do aplikacji, należy utworzyć reguły grupy zabezpieczeń sieci z [AzureRmNetworkSecurityRuleConfig nowy](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="60e0f-158">To allow web traffic to reach your app, create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="60e0f-159">Poniższy przykład tworzy regułę grupy zabezpieczeń sieci o nazwie `myNetworkSecurityGroupRule`:</span><span class="sxs-lookup"><span data-stu-id="60e0f-159">The following example creates a network security group rule named `myNetworkSecurityGroupRule`:</span></span>

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow
```

<span data-ttu-id="60e0f-160">Utwórz grupę zabezpieczeń sieci z [AzureRmNetworkSecurityGroup nowy](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="60e0f-160">Create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="60e0f-161">Poniższy przykład tworzy grupy NSG o nazwie `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="60e0f-161">The following example creates an NSG named `myNetworkSecurityGroup`:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

<span data-ttu-id="60e0f-162">Dodaj sieciową grupę zabezpieczeń do podsieci o [AzureRmVirtualNetworkSubnetConfig zestaw](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="60e0f-162">Add the network security group to the subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="60e0f-163">Aktualizacja sieci wirtualnej z [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="60e0f-163">Update the virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a><span data-ttu-id="60e0f-164">Utwórz sieć wirtualną kartami interfejsu</span><span class="sxs-lookup"><span data-stu-id="60e0f-164">Create virtual network interface cards</span></span>

<span data-ttu-id="60e0f-165">Załadować funkcji równoważenia zasobu wirtualnego karty Sieciowej, a nie rzeczywiste maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="60e0f-165">Load balancers function with the virtual NIC resource rather than the actual VM.</span></span> <span data-ttu-id="60e0f-166">Wirtualnej karty Sieciowej jest połączone z usługą równoważenia obciążenia, a następnie dołączony do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="60e0f-166">The virtual NIC is connected to the load balancer, and then attached to a VM.</span></span>

<span data-ttu-id="60e0f-167">Tworzenie wirtualnej karty Sieciowej z [AzureRmNetworkInterface nowy](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="60e0f-167">Create a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="60e0f-168">Poniższy przykład tworzy trzy wirtualne karty sieciowe.</span><span class="sxs-lookup"><span data-stu-id="60e0f-168">The following example creates three virtual NICs.</span></span> <span data-ttu-id="60e0f-169">(Jedną wirtualną kartę Sieciową dla każdej maszyny Wirtualnej jest tworzona dla aplikacji w poniższych krokach):</span><span class="sxs-lookup"><span data-stu-id="60e0f-169">(One virtual NIC for each VM you create for your app in the following steps):</span></span>


```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface -ResourceGroupName myResourceGroup `
     -Name myNic$i `
     -Location westeurope `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}

```

## <a name="step-5---create-virtual-machines"></a><span data-ttu-id="60e0f-170">Krok 5 — Tworzenie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="60e0f-170">Step 5 - Create virtual machines</span></span>

<span data-ttu-id="60e0f-171">Wszystkie składniki w miejscu można teraz tworzyć maszyny wirtualne o wysokiej dostępności do uruchomienia aplikacji sieci.</span><span class="sxs-lookup"><span data-stu-id="60e0f-171">With all the underlying components in place, you can now create highly available VMs to run your app.</span></span> 

<span data-ttu-id="60e0f-172">Pobierz nazwę użytkownika i hasło potrzebne do konta administratora na maszynie wirtualnej z [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="60e0f-172">Get the username and password needed for the administrator account on the virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="60e0f-173">Tworzenie maszyn wirtualnych o [nowe AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [AzureRmVMOperatingSystem zestaw](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [AzureRmVMSourceImage zestaw](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [AzureRmVMOSDisk zestaw](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [AzureRmVMNetworkInterface dodać](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), i [nowe AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="60e0f-173">Create the VMs with [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="60e0f-174">Poniższy przykład tworzy trzech maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="60e0f-174">The following example creates three VMs:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   $vm = New-AzureRmVMConfig -VMName myVM$i -VMSize Standard_D1 -AvailabilitySetId $availabilitySet.Id
   $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName myVM$i -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version latest
   $vm = Set-AzureRmVMOSDisk -VM $vm -Name myOsDisk$i -StorageAccountType StandardLRS -DiskSizeInGB 128 -CreateOption FromImage -Caching ReadWrite
   $nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic$i
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vm
}

```

<span data-ttu-id="60e0f-175">Trwa kilka minut, aby utworzyć i skonfigurować wszystkie trzy maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="60e0f-175">It takes several minutes to create and configure all three VMs.</span></span> <span data-ttu-id="60e0f-176">Sondy kondycji modułu równoważenia obciążenia automatycznie wykrywa, gdy aplikacja jest uruchomiona na każdej maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="60e0f-176">The load balancer health probe automatically detects when the app is running on each VM.</span></span> <span data-ttu-id="60e0f-177">Gdy aplikacja jest uruchomiona, rozpoczyna się reguły modułu równoważenia obciążenia do dystrybucji ruchu.</span><span class="sxs-lookup"><span data-stu-id="60e0f-177">Once the app is running, the load balancer rule starts to distribute traffic.</span></span>

### <a name="install-the-app"></a><span data-ttu-id="60e0f-178">Zainstaluj aplikację</span><span class="sxs-lookup"><span data-stu-id="60e0f-178">Install the app</span></span> 

<span data-ttu-id="60e0f-179">Rozszerzenia maszyny wirtualnej platformy Azure są używane do automatyzowania zadań konfiguracji maszyny wirtualnej, takie jak instalowanie aplikacji i konfigurowanie systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="60e0f-179">Azure virtual machine extensions are used to automate virtual machine configuration tasks such as installing applications and configuring the operating system.</span></span> <span data-ttu-id="60e0f-180">[Niestandardowe rozszerzenie skryptu dla systemu Windows](./../virtual-machines-windows-extensions-customscript.md) służy do uruchomienia dowolnego skryptu programu PowerShell na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="60e0f-180">The [custom script extension for Windows](./../virtual-machines-windows-extensions-customscript.md) is used to run any PowerShell script on the virtual machine.</span></span> <span data-ttu-id="60e0f-181">Skrypt można przechowywane w magazynie Azure, wszelkie dostępny punkt końcowy HTTP lub osadzone w konfiguracji rozszerzenia niestandardowego skryptu.</span><span class="sxs-lookup"><span data-stu-id="60e0f-181">The script can be stored in Azure storage, any accessible HTTP endpoint, or embedded in the custom script extension configuration.</span></span> <span data-ttu-id="60e0f-182">Podczas korzystania z niestandardowego rozszerzenia skryptu, agent maszyny Wirtualnej platformy Azure zarządza wykonania skryptu.</span><span class="sxs-lookup"><span data-stu-id="60e0f-182">When using the custom script extension, the Azure VM agent manages the script execution.</span></span>

<span data-ttu-id="60e0f-183">Użyj [AzureRmVMExtension zestaw](/powershell/module/azurerm.compute/set-azurermvmextension) można zainstalować rozszerzenia niestandardowego skryptu.</span><span class="sxs-lookup"><span data-stu-id="60e0f-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) to install the custom script extension.</span></span> <span data-ttu-id="60e0f-184">Uruchamia rozszerzenia `powershell Add-WindowsFeature Web-Server` Aby zainstalować serwer sieci Web usług IIS:</span><span class="sxs-lookup"><span data-stu-id="60e0f-184">The extension runs `powershell Add-WindowsFeature Web-Server` to install the IIS webserver:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server"}' `
     -Location westeurope
}
```

### <a name="test-your-app"></a><span data-ttu-id="60e0f-185">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="60e0f-185">Test your app</span></span>

<span data-ttu-id="60e0f-186">Publiczny adres IP z usługi równoważenia obciążenia z [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="60e0f-186">Obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="60e0f-187">Poniższy przykład uzyskuje adres IP dla `myPublicIP` utworzony wcześniej:</span><span class="sxs-lookup"><span data-stu-id="60e0f-187">The following example obtains the IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

<span data-ttu-id="60e0f-188">Wprowadź publicznego adresu IP w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="60e0f-188">Enter the public IP address in to a web browser.</span></span> <span data-ttu-id="60e0f-189">Reguły NSG w miejscu wyświetlane jest IIS domyślnej witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="60e0f-189">With the NSG rule in place, the default IIS website is displayed.</span></span> 

![Domyślna witryna usług IIS](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a><span data-ttu-id="60e0f-191">Krok 6 — zadania związane z zarządzaniem</span><span class="sxs-lookup"><span data-stu-id="60e0f-191">Step 6 – Management tasks</span></span>

<span data-ttu-id="60e0f-192">Może być konieczne przeprowadzenie konserwacji na maszynach wirtualnych z tą aplikacją, takich jak instalowanie aktualizacji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="60e0f-192">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="60e0f-193">Aby poradzić sobie z zwiększenie obciążenia do aplikacji, może być konieczne dodanie kolejnych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="60e0f-193">To deal with increased traffic to your app, you may need to add additional VMs.</span></span> <span data-ttu-id="60e0f-194">W tej sekcji przedstawiono sposób Usuń lub Dodaj Maszynę wirtualną z modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="60e0f-194">This section shows you how to remove or add a VM from the load balancer.</span></span> 

### <a name="remove-a-vm-from-the-load-balancer"></a><span data-ttu-id="60e0f-195">Usuń Maszynę wirtualną z usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="60e0f-195">Remove a VM from the load balancer</span></span>

<span data-ttu-id="60e0f-196">Usuń Maszynę wirtualną z puli adresów zaplecza resetując właściwość Loadbalancerbackendaddresspool karty interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="60e0f-196">Remove a VM from the backend address pool by resetting the LoadBalancerBackendAddressPools property of the network interface card.</span></span>

<span data-ttu-id="60e0f-197">Pobierz karty interfejsu sieciowego z [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="60e0f-197">Get the network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

<span data-ttu-id="60e0f-198">Ustaw właściwość Loadbalancerbackendaddresspool karty interfejsu sieciowego na $null:</span><span class="sxs-lookup"><span data-stu-id="60e0f-198">Set the LoadBalancerBackendAddressPools property of the network interface card to $null:</span></span>

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

<span data-ttu-id="60e0f-199">Aktualizacja karty interfejsu sieciowego:</span><span class="sxs-lookup"><span data-stu-id="60e0f-199">Update the network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-to-the-load-balancer"></a><span data-ttu-id="60e0f-200">Dodaj Maszynę wirtualną z usługą równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="60e0f-200">Add a VM to the load balancer</span></span>

<span data-ttu-id="60e0f-201">Po konserwacja maszyny Wirtualnej, lub jeśli trzeba zwiększyć pojemność, dodanie karty Sieciowej maszyny wirtualnej do puli adresów zaplecza modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="60e0f-201">After performing VM maintenance, or if you need to expand capacity, adding the NIC of a VM to the backend address pool of the load balancer.</span></span>

<span data-ttu-id="60e0f-202">Pobierz moduł równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="60e0f-202">Get the load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

<span data-ttu-id="60e0f-203">Dodaj puli adresów zaplecza modułu równoważenia obciążenia do karty interfejsu sieciowego:</span><span class="sxs-lookup"><span data-stu-id="60e0f-203">Add the backend address pool of the load balancer to the network interface card:</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

<span data-ttu-id="60e0f-204">Aktualizacja karty interfejsu sieciowego:</span><span class="sxs-lookup"><span data-stu-id="60e0f-204">Update the network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="60e0f-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="60e0f-205">Next Steps</span></span>

<span data-ttu-id="60e0f-206">Przykłady — [programu Azure PowerShell maszyny wirtualnej przykładowe skrypty](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="60e0f-206">Samples – [Azure Virtual Machine PowerShell sample scripts](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
