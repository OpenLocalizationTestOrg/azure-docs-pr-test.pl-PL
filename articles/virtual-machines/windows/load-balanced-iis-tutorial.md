---
title: "aaaTutorial - kompilacji wysoką dostępność aplikacji na maszynach wirtualnych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate wysokiej dostępności i bezpieczne aplikacji w trzech maszyn wirtualnych systemu Windows z usługą równoważenia obciążenia na platformie Azure"
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
ms.openlocfilehash: f9eff96be4f3999651c4108f0334e4eaa1a39c0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a><span data-ttu-id="99307-103">Tworzenie równoważone, wysoką dostępność aplikacji na maszynach wirtualnych systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="99307-103">Build a load balanced, highly available application on Windows virtual machines in Azure</span></span>

<span data-ttu-id="99307-104">W tym samouczku utworzysz wysokiej dostępności aplikacji, która jest odporność toomaintenance zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="99307-104">In this tutorial, you create a highly available application that is resilient toomaintenance events.</span></span> <span data-ttu-id="99307-105">Aplikacja Hello używa modułu równoważenia obciążenia, zestawu dostępności i trzech maszyn wirtualnych systemu Windows (VM).</span><span class="sxs-lookup"><span data-stu-id="99307-105">hello app uses a load balancer, an availability set, and three Windows virtual machines (VMs).</span></span> <span data-ttu-id="99307-106">W tym samouczku instaluje usługi IIS, chociaż można użyć tego samouczka toodeploy framework innej aplikacji przy użyciu hello same składniki wysokiej dostępności i wytyczne.</span><span class="sxs-lookup"><span data-stu-id="99307-106">This tutorial installs IIS, though you can use this tutorial toodeploy a different application framework using hello same high availability components and guidelines.</span></span> 

## <a name="step-1---azure-prerequisites"></a><span data-ttu-id="99307-107">Krok 1 — wymagania wstępne platformy Azure</span><span class="sxs-lookup"><span data-stu-id="99307-107">Step 1 - Azure prerequisites</span></span>

<span data-ttu-id="99307-108">toocomplete tego samouczka, upewnij się, czy hello zostały zainstalowane najnowsze [programu Azure PowerShell](/powershell/azure/overview) modułu.</span><span class="sxs-lookup"><span data-stu-id="99307-108">toocomplete this tutorial, make sure that you have installed hello latest [Azure PowerShell](/powershell/azure/overview) module.</span></span>

<span data-ttu-id="99307-109">Po pierwsze Zaloguj się za tooyour subskrypcji platformy Azure z hello polecenia Login-AzureRmAccount i wykonaj hello wyświetlanymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="99307-109">First, log in tooyour Azure subscription with hello Login-AzureRmAccount command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="99307-110">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="99307-110">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="99307-111">Przed utworzeniem innych zasobów platformy Azure, należy toocreate grupą zasobów o [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="99307-111">Before you can create any other Azure resources, you need toocreate a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="99307-112">Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `westeurope` regionu:</span><span class="sxs-lookup"><span data-stu-id="99307-112">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` region:</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a><span data-ttu-id="99307-113">Krok 2 — Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="99307-113">Step 2 - Create availability set</span></span>

<span data-ttu-id="99307-114">Maszyny wirtualne mogą być tworzone przez błędów logicznych i Aktualizacja domeny.</span><span class="sxs-lookup"><span data-stu-id="99307-114">Virtual machines can be created across logical fault and update domains.</span></span> <span data-ttu-id="99307-115">Każdej domeny logicznej reprezentuje część sprzętu w centrum danych Azure podstawowej hello.</span><span class="sxs-lookup"><span data-stu-id="99307-115">Each logical domain represents a portion of hardware in hello underlying Azure datacenter.</span></span> <span data-ttu-id="99307-116">Po utworzeniu co najmniej dwie maszyny wirtualne, zasobów obliczeniowych i przestrzeni dyskowej są dystrybuowane w tych domenach.</span><span class="sxs-lookup"><span data-stu-id="99307-116">When you create two or more VMs, your compute and storage resources are distributed across these domains.</span></span> <span data-ttu-id="99307-117">Tej dystrybucji przechowuje hello dostępność aplikacji, jeśli składnik sprzętowy wymaga konserwacji.</span><span class="sxs-lookup"><span data-stu-id="99307-117">This distribution maintains hello availability of your app if a hardware component needs maintenance.</span></span> <span data-ttu-id="99307-118">Zestawy dostępności umożliwiają zdefiniowanie tych logicznej domen błędów i aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="99307-118">Availability sets let you define these logical fault and update domains.</span></span>

<span data-ttu-id="99307-119">Utwórz zestaw o dostępności [AzureRmAvailabilitySet nowy](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="99307-119">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="99307-120">Witaj poniższy przykład tworzy zbiór nazwanego dostępności `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="99307-120">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a><span data-ttu-id="99307-121">Krok 3 — Tworzenie obciążenia równoważenia</span><span class="sxs-lookup"><span data-stu-id="99307-121">Step 3 - Create load balancer</span></span>

<span data-ttu-id="99307-122">Moduł równoważenia obciążenia Azure dystrybuuje ruch zestawu zdefiniowanego maszyn wirtualnych przy użyciu reguły modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="99307-122">An Azure load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="99307-123">Sondy kondycji monitoruje danego portu na każdej maszynie Wirtualnej, a tylko dystrybuuje ruch tooan operacyjne maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="99307-123">A health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

### <a name="create-public-ip-address"></a><span data-ttu-id="99307-124">Utwórz publiczny adres IP</span><span class="sxs-lookup"><span data-stu-id="99307-124">Create public IP address</span></span>

<span data-ttu-id="99307-125">tooaccess aplikacji na powitania Internet, przypisz publicznego równoważenia obciążenia toohello adresów IP.</span><span class="sxs-lookup"><span data-stu-id="99307-125">tooaccess your app on hello Internet, assign a public IP address toohello load balancer.</span></span> <span data-ttu-id="99307-126">Utwórz publiczny adres IP z [AzureRmPublicIpAddress nowy](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="99307-126">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="99307-127">Witaj poniższy przykład tworzy publiczny adres IP o nazwie `myPublicIP`:</span><span class="sxs-lookup"><span data-stu-id="99307-127">hello following example creates a public IP address named `myPublicIP`:</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a><span data-ttu-id="99307-128">Tworzenie usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="99307-128">Create load balancer</span></span>

<span data-ttu-id="99307-129">Utwórz na adres IP frontonu [AzureRmLoadBalancerFrontendIpConfig nowy](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="99307-129">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="99307-130">Witaj poniższy przykład tworzy adresu IP serwera sieci Web o nazwie `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="99307-130">hello following example creates a frontend IP address named `myFrontEndPool`:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

<span data-ttu-id="99307-131">Utwórz pulę adresów zaplecza z [AzureRmLoadBalancerBackendAddressPoolConfig nowy](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="99307-131">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="99307-132">Witaj poniższy przykład tworzy puli adresów zaplecza, o nazwie `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="99307-132">hello following example creates a backend address pool named `myBackEndPool`:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="99307-133">Teraz utworzymy hello modułu równoważenia obciążenia z [AzureRmLoadBalancer nowy](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="99307-133">Now, create hello load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="99307-134">Witaj poniższy przykład tworzy moduł równoważenia obciążenia o nazwie `myLoadBalancer` przy użyciu hello `myPublicIP` adres:</span><span class="sxs-lookup"><span data-stu-id="99307-134">hello following example creates a load balancer named `myLoadBalancer` using hello `myPublicIP` address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a><span data-ttu-id="99307-135">Utworzyć sondy kondycji</span><span class="sxs-lookup"><span data-stu-id="99307-135">Create health probe</span></span>

<span data-ttu-id="99307-136">tooallow hello stanu usługi równoważenia obciążenia toomonitor hello aplikacji, możesz użyć sondy kondycji.</span><span class="sxs-lookup"><span data-stu-id="99307-136">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="99307-137">sondy kondycji Hello dynamicznie dodaje lub usuwa maszyn wirtualnych z obrotu usługi równoważenia obciążenia hello oparte na ich kontroli toohealth odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="99307-137">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="99307-138">Domyślnie maszyny Wirtualnej zostanie usunięte z dystrybucji modułu równoważenia obciążenia powitania po dwóch kolejnych błędów na 15 sekund.</span><span class="sxs-lookup"><span data-stu-id="99307-138">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span>

<span data-ttu-id="99307-139">Utwórz badanie kondycji z [AzureRmLoadBalancerProbeConfig Dodaj](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="99307-139">Create a health probe with [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="99307-140">Witaj poniższy przykład tworzy badanie kondycji o nazwie `myHealthProbe` który monitoruje każdej maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="99307-140">hello following example creates a health probe named `myHealthProbe` that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a><span data-ttu-id="99307-141">Tworzenie reguły modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="99307-141">Create load balancer rule</span></span>

<span data-ttu-id="99307-142">Reguły modułu równoważenia obciążenia jest używany toodefine sposób ruch jest rozproszonej toohello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="99307-142">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span>

<span data-ttu-id="99307-143">Tworzenie reguły modułu równoważenia obciążenia z [AzureRmLoadBalancerRuleConfig Dodaj](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="99307-143">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="99307-144">Witaj poniższy przykład tworzy regułę równoważenia obciążenia o nazwie `myLoadBalancerRule` i równoważy ruch na porcie `80`:</span><span class="sxs-lookup"><span data-stu-id="99307-144">hello following example creates a load balancer rule named `myLoadBalancerRule` and balances traffic on port `80`:</span></span>

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

<span data-ttu-id="99307-145">Zaktualizuj hello modułu równoważenia obciążenia z [AzureRmLoadBalancer zestaw](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="99307-145">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a><span data-ttu-id="99307-146">Krok 4 — Konfigurowanie sieci</span><span class="sxs-lookup"><span data-stu-id="99307-146">Step 4 - Configure networking</span></span>

<span data-ttu-id="99307-147">Każda maszyna wirtualna ma co najmniej jeden wirtualny kart interfejsu sieciowego (NIC) łączących tooa sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="99307-147">Each VM has one or more virtual network interface cards (NICs) that connect tooa virtual network.</span></span> <span data-ttu-id="99307-148">Ta sieć wirtualna jest chroniona toofilter ruchu na podstawie reguł zdefiniowanych dostępu.</span><span class="sxs-lookup"><span data-stu-id="99307-148">This virtual network is secured toofilter traffic based on defined access rules.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="99307-149">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="99307-149">Create virtual network</span></span>

<span data-ttu-id="99307-150">Skonfiguruj podsieci z [AzureRmVirtualNetworkSubnetConfig nowy](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="99307-150">First, configure a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="99307-151">Witaj poniższy przykład tworzy podsieć o nazwie `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="99307-151">hello following example creates a subnet named `mySubnet`:</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="99307-152">tooyour łączności sieciowej tooprovide maszyn wirtualnych, Utwórz sieć wirtualną z [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="99307-152">tooprovide network connectivity tooyour VMs, create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="99307-153">Witaj poniższy przykład tworzy sieć wirtualną o nazwie `myVnet` z `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="99307-153">hello following example creates a virtual network named `myVnet` with `mySubnet`:</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a><span data-ttu-id="99307-154">Konfigurowanie zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="99307-154">Configure network security</span></span>

<span data-ttu-id="99307-155">Azure [sieciowej grupy zabezpieczeń](../../virtual-network/virtual-networks-nsg.md) (NSG) steruje ruchu przychodzącego i wychodzącego dla jednego lub wielu maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="99307-155">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="99307-156">Reguły grupy zabezpieczeń sieci akceptować lub odrzucać ruchu sieciowego na określonym porcie lub zakres portów.</span><span class="sxs-lookup"><span data-stu-id="99307-156">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="99307-157">Te zasady mogą również obejmować prefiks adresu źródłowego, dzięki czemu tylko ruch w źródle wstępnie zdefiniowanych może komunikować się z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="99307-157">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span>

<span data-ttu-id="99307-158">tooallow aplikacji sieci web tooreach ruchu, należy utworzyć reguły grupy zabezpieczeń sieci z [AzureRmNetworkSecurityRuleConfig nowy](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="99307-158">tooallow web traffic tooreach your app, create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="99307-159">Witaj poniższy przykład tworzy regułę grupy zabezpieczeń sieci o nazwie `myNetworkSecurityGroupRule`:</span><span class="sxs-lookup"><span data-stu-id="99307-159">hello following example creates a network security group rule named `myNetworkSecurityGroupRule`:</span></span>

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

<span data-ttu-id="99307-160">Utwórz grupę zabezpieczeń sieci z [AzureRmNetworkSecurityGroup nowy](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="99307-160">Create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="99307-161">Witaj poniższy przykład tworzy grupy NSG o nazwie `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="99307-161">hello following example creates an NSG named `myNetworkSecurityGroup`:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

<span data-ttu-id="99307-162">Dodaj podsieć toohello grupy zabezpieczeń sieci hello z [AzureRmVirtualNetworkSubnetConfig zestaw](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="99307-162">Add hello network security group toohello subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="99307-163">Aktualizacja sieci wirtualnej hello o [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="99307-163">Update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a><span data-ttu-id="99307-164">Utwórz sieć wirtualną kartami interfejsu</span><span class="sxs-lookup"><span data-stu-id="99307-164">Create virtual network interface cards</span></span>

<span data-ttu-id="99307-165">Ładowanie funkcji równoważenia z hello wirtualnej karty Sieciowej zasobów zamiast hello rzeczywiste maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="99307-165">Load balancers function with hello virtual NIC resource rather than hello actual VM.</span></span> <span data-ttu-id="99307-166">Hello wirtualnej karty Sieciowej podłączonej toohello Usługa równoważenia obciążenia, a następnie dołączony tooa maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="99307-166">hello virtual NIC is connected toohello load balancer, and then attached tooa VM.</span></span>

<span data-ttu-id="99307-167">Tworzenie wirtualnej karty Sieciowej z [AzureRmNetworkInterface nowy](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="99307-167">Create a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="99307-168">Witaj poniższy przykład tworzy trzy wirtualne karty sieciowe.</span><span class="sxs-lookup"><span data-stu-id="99307-168">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="99307-169">(Jedną wirtualną kartę Sieciową dla każdej maszyny Wirtualnej jest tworzona dla aplikacji w hello następujące kroki):</span><span class="sxs-lookup"><span data-stu-id="99307-169">(One virtual NIC for each VM you create for your app in hello following steps):</span></span>


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

## <a name="step-5---create-virtual-machines"></a><span data-ttu-id="99307-170">Krok 5 — Tworzenie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="99307-170">Step 5 - Create virtual machines</span></span>

<span data-ttu-id="99307-171">Z wszystkich hello podstawowych składników w miejscu można teraz utworzyć toorun maszyn wirtualnych wysokiej dostępności aplikacji.</span><span class="sxs-lookup"><span data-stu-id="99307-171">With all hello underlying components in place, you can now create highly available VMs toorun your app.</span></span> 

<span data-ttu-id="99307-172">Pobierz hello nazwę użytkownika i hasło potrzebne do konta administratora hello na maszynie wirtualnej hello [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="99307-172">Get hello username and password needed for hello administrator account on hello virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="99307-173">Tworzenie maszyn wirtualnych hello z [AzureRmVMConfig nowy](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [AzureRmVMOperatingSystem zestaw](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [AzureRmVMSourceImage zestaw](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Dodać AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), i [nowe AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="99307-173">Create hello VMs with [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="99307-174">Witaj poniższy przykład tworzy trzech maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="99307-174">hello following example creates three VMs:</span></span>

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

<span data-ttu-id="99307-175">Go zajmuje kilka minut toocreate i skonfiguruj wszystkie trzy maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="99307-175">It takes several minutes toocreate and configure all three VMs.</span></span> <span data-ttu-id="99307-176">Witaj sondy kondycji modułu równoważenia obciążenia automatycznie wykrywa aplikacji hello jest uruchomiona na każdej maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="99307-176">hello load balancer health probe automatically detects when hello app is running on each VM.</span></span> <span data-ttu-id="99307-177">Po uruchomieniu aplikacji hello reguły modułu równoważenia obciążenia hello uruchamia toodistribute ruchu.</span><span class="sxs-lookup"><span data-stu-id="99307-177">Once hello app is running, hello load balancer rule starts toodistribute traffic.</span></span>

### <a name="install-hello-app"></a><span data-ttu-id="99307-178">Instalowanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="99307-178">Install hello app</span></span> 

<span data-ttu-id="99307-179">Zadania konfiguracji maszyny wirtualnej tooautomate używane, takie jak instalowanie aplikacji i konfigurowanie systemu operacyjnego hello są rozszerzenia maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="99307-179">Azure virtual machine extensions are used tooautomate virtual machine configuration tasks such as installing applications and configuring hello operating system.</span></span> <span data-ttu-id="99307-180">Witaj [niestandardowe rozszerzenie skryptu dla systemu Windows](./../virtual-machines-windows-extensions-customscript.md) jest używane toorun dowolny skrypt programu PowerShell na maszynie wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="99307-180">hello [custom script extension for Windows](./../virtual-machines-windows-extensions-customscript.md) is used toorun any PowerShell script on hello virtual machine.</span></span> <span data-ttu-id="99307-181">skrypt Hello można przechowywane w magazynie Azure, wszelkie dostępny punkt końcowy HTTP lub osadzone w konfiguracji rozszerzenia niestandardowego skryptu hello.</span><span class="sxs-lookup"><span data-stu-id="99307-181">hello script can be stored in Azure storage, any accessible HTTP endpoint, or embedded in hello custom script extension configuration.</span></span> <span data-ttu-id="99307-182">Używając hello niestandardowe rozszerzenie skryptu, agent maszyny Wirtualnej Azure hello zarządza hello wykonywanie skryptu.</span><span class="sxs-lookup"><span data-stu-id="99307-182">When using hello custom script extension, hello Azure VM agent manages hello script execution.</span></span>

<span data-ttu-id="99307-183">Użyj [AzureRmVMExtension zestaw](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello niestandardowego rozszerzenia skryptu.</span><span class="sxs-lookup"><span data-stu-id="99307-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello custom script extension.</span></span> <span data-ttu-id="99307-184">Witaj uruchamia rozszerzenia `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS serwer sieci Web:</span><span class="sxs-lookup"><span data-stu-id="99307-184">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver:</span></span>

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

### <a name="test-your-app"></a><span data-ttu-id="99307-185">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="99307-185">Test your app</span></span>

<span data-ttu-id="99307-186">Uzyskaj hello publicznego adresu IP z usługi równoważenia obciążenia z [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="99307-186">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="99307-187">Witaj poniższy przykład uzyskuje hello adres IP dla `myPublicIP` utworzony wcześniej:</span><span class="sxs-lookup"><span data-stu-id="99307-187">hello following example obtains hello IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

<span data-ttu-id="99307-188">Wprowadź hello publicznego adresu IP w przeglądarce sieci web tooa.</span><span class="sxs-lookup"><span data-stu-id="99307-188">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="99307-189">Reguły NSG hello w miejscu hello domyślna witryna sieci Web IIS są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="99307-189">With hello NSG rule in place, hello default IIS website is displayed.</span></span> 

![Domyślna witryna usług IIS](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a><span data-ttu-id="99307-191">Krok 6 — zadania związane z zarządzaniem</span><span class="sxs-lookup"><span data-stu-id="99307-191">Step 6 – Management tasks</span></span>

<span data-ttu-id="99307-192">Może być konieczne tooperform konserwacji na powitania maszyn wirtualnych z tą aplikacją, takich jak instalowanie aktualizacji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="99307-192">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="99307-193">toodeal z aplikacją tooyour zwiększenie obciążenia, może być konieczne tooadd kolejnych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="99307-193">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="99307-194">W tej sekcji opisano sposób tooremove lub dodać maszyny Wirtualnej z hello modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="99307-194">This section shows you how tooremove or add a VM from hello load balancer.</span></span> 

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="99307-195">Usuń Maszynę wirtualną z hello modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="99307-195">Remove a VM from hello load balancer</span></span>

<span data-ttu-id="99307-196">Usuń Maszynę wirtualną z puli adresów zaplecza hello resetując właściwość Loadbalancerbackendaddresspool hello hello karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="99307-196">Remove a VM from hello backend address pool by resetting hello LoadBalancerBackendAddressPools property of hello network interface card.</span></span>

<span data-ttu-id="99307-197">Pobierz hello karty interfejsu sieciowego z [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="99307-197">Get hello network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

<span data-ttu-id="99307-198">Ustaw właściwość Loadbalancerbackendaddresspool hello karty interfejsu sieciowego hello zbyt$ null:</span><span class="sxs-lookup"><span data-stu-id="99307-198">Set hello LoadBalancerBackendAddressPools property of hello network interface card too$null:</span></span>

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

<span data-ttu-id="99307-199">Karty interfejsu sieciowego hello aktualizacji:</span><span class="sxs-lookup"><span data-stu-id="99307-199">Update hello network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="99307-200">Dodaj usługi równoważenia obciążenia toohello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="99307-200">Add a VM toohello load balancer</span></span>

<span data-ttu-id="99307-201">Po konserwacja maszyny Wirtualnej lub tooexpand pojemności należy dodawanie hello karty Sieciowej maszyny Wirtualnej puli adresów zaplecza toohello hello usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="99307-201">After performing VM maintenance, or if you need tooexpand capacity, adding hello NIC of a VM toohello backend address pool of hello load balancer.</span></span>

<span data-ttu-id="99307-202">Pobierz hello usługi równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="99307-202">Get hello load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

<span data-ttu-id="99307-203">Dodaj hello puli adresów zaplecza modułu równoważenia obciążenia hello toohello karty interfejsu sieciowego:</span><span class="sxs-lookup"><span data-stu-id="99307-203">Add hello backend address pool of hello load balancer toohello network interface card:</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

<span data-ttu-id="99307-204">Karty interfejsu sieciowego hello aktualizacji:</span><span class="sxs-lookup"><span data-stu-id="99307-204">Update hello network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="99307-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="99307-205">Next Steps</span></span>

<span data-ttu-id="99307-206">Przykłady — [programu Azure PowerShell maszyny wirtualnej przykładowe skrypty](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="99307-206">Samples – [Azure Virtual Machine PowerShell sample scripts](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
