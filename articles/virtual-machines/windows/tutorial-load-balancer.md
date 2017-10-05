---
title: "Jak załadować saldo maszyn wirtualnych systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać usługi równoważenia obciążenia Azure do tworzenia aplikacji wysokiej dostępności i bezpieczne w trzech maszyn wirtualnych systemu Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 6738d88d5a0430abaf3855dbf97a618e4c83617f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-load-balance-windows-virtual-machines-in-azure-to-create-a-highly-available-application"></a><span data-ttu-id="959f0-103">Jak załadować saldo maszyn wirtualnych systemu Windows na platformie Azure, aby utworzyć aplikację wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="959f0-103">How to load balance Windows virtual machines in Azure to create a highly available application</span></span>
<span data-ttu-id="959f0-104">Równoważenie obciążenia sieciowego zapewnia wyższy poziom dostępności dzięki rozproszeniu przychodzące żądania między wieloma maszynami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="959f0-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="959f0-105">W tym samouczku opisano różne składniki usługi równoważenia obciążenia Azure dystrybucji ruchu, które zapewniają wysoką dostępność.</span><span class="sxs-lookup"><span data-stu-id="959f0-105">In this tutorial, you learn about the different components of the Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="959f0-106">Omawiane kwestie:</span><span class="sxs-lookup"><span data-stu-id="959f0-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="959f0-107">Tworzenie usługi równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="959f0-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="959f0-108">Utwórz kondycji sondę modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="959f0-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="959f0-109">Tworzenie reguły ruchu usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="959f0-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="959f0-110">Niestandardowe rozszerzenie skryptu umożliwiają utworzenie podstawowej witryny usług IIS</span><span class="sxs-lookup"><span data-stu-id="959f0-110">Use the Custom Script Extension to create a basic IIS site</span></span>
> * <span data-ttu-id="959f0-111">Tworzenie maszyn wirtualnych i dołączanie do usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="959f0-111">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="959f0-112">Wyświetl modułu równoważenia obciążenia w akcji</span><span class="sxs-lookup"><span data-stu-id="959f0-112">View a load balancer in action</span></span>
> * <span data-ttu-id="959f0-113">Dodawanie i usuwanie maszyny wirtualne z modułem równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="959f0-113">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="959f0-114">Dla tego samouczka jest wymagany moduł Azure PowerShell w wersji 3.6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="959f0-114">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="959f0-115">Uruchom polecenie ` Get-Module -ListAvailable AzureRM`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="959f0-115">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="959f0-116">Jeśli potrzebujesz do uaktualnienia, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="959f0-116">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="azure-load-balancer-overview"></a><span data-ttu-id="959f0-117">Omówienie usługi równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="959f0-117">Azure load balancer overview</span></span>
<span data-ttu-id="959f0-118">Moduł równoważenia obciążenia Azure jest równoważenia obciążenia warstwy 4 (TCP, UDP), który zapewnia wysoką dostępność, przekazując przychodzący ruch między maszynami wirtualnymi w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="959f0-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="959f0-119">Badanie kondycji modułu równoważenia obciążenia monitoruje danego portu na każdej maszynie Wirtualnej i tylko dystrybuuje ruch do operacyjnej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="959f0-119">A load balancer health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span>

<span data-ttu-id="959f0-120">Należy zdefiniować frontonu konfiguracji adresu IP, który zawiera co najmniej jeden publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="959f0-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="959f0-121">Ta frontonu konfiguracji IP umożliwia Twojej usługi równoważenia obciążenia i aplikacje mają być dostępne za pośrednictwem Internetu.</span><span class="sxs-lookup"><span data-stu-id="959f0-121">This front-end IP configuration allows your load balancer and applications to be accessible over the Internet.</span></span> 

<span data-ttu-id="959f0-122">Maszyny wirtualne połączenia z modułem równoważenia obciążenia przy użyciu ich karty interfejsu sieci wirtualnej (NIC).</span><span class="sxs-lookup"><span data-stu-id="959f0-122">Virtual machines connect to a load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="959f0-123">Aby rozpowszechnić ruch do maszyn wirtualnych, puli adresów zaplecza zawiera adres IP adresów wirtualnych (NIC) połączony z usługą równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="959f0-123">To distribute traffic to the VMs, a back-end address pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span></span>

<span data-ttu-id="959f0-124">Aby sterowanie przepływem ruchu, należy zdefiniować reguły modułu równoważenia obciążenia dla określonych portów i protokołów, które mapują do maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="959f0-124">To control the flow of traffic, you define load balancer rules for specific ports and protocols that map to your VMs.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="959f0-125">Tworzenie usługi równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="959f0-125">Create Azure load balancer</span></span>
<span data-ttu-id="959f0-126">W tej sekcji Szczegóły, jak można tworzyć i konfigurować poszczególnych składników usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="959f0-126">This section details how you can create and configure each component of the load balancer.</span></span> <span data-ttu-id="959f0-127">Przed utworzeniem przez moduł równoważenia obciążenia, Utwórz nową grupę zasobów o [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="959f0-127">Before you can create your load balancer, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="959f0-128">Poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupLoadBalancer* w *EastUS* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="959f0-128">The following example creates a resource group named *myResourceGroupLoadBalancer* in the *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="959f0-129">Tworzenie publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="959f0-129">Create a public IP address</span></span>
<span data-ttu-id="959f0-130">Aby uzyskać dostęp do aplikacji w Internecie, należy publicznego adresu IP usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="959f0-130">To access your app on the Internet, you need a public IP address for the load balancer.</span></span> <span data-ttu-id="959f0-131">Utwórz publiczny adres IP z [AzureRmPublicIpAddress nowy](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="959f0-131">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="959f0-132">Poniższy przykład tworzy publiczny adres IP o nazwie *myPublicIP* w *myResourceGroupLoadBalancer* grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="959f0-132">The following example creates a public IP address named *myPublicIP* in the *myResourceGroupLoadBalancer* resource group:</span></span>

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="959f0-133">Tworzenie modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="959f0-133">Create a load balancer</span></span>
<span data-ttu-id="959f0-134">Utwórz na adres IP frontonu [AzureRmLoadBalancerFrontendIpConfig nowy](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="959f0-134">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="959f0-135">Poniższy przykład tworzy adresu IP serwera sieci Web o nazwie *myFrontEndPool*:</span><span class="sxs-lookup"><span data-stu-id="959f0-135">The following example creates a frontend IP address named *myFrontEndPool*:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

<span data-ttu-id="959f0-136">Utwórz pulę adresów zaplecza z [AzureRmLoadBalancerBackendAddressPoolConfig nowy](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="959f0-136">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="959f0-137">Poniższy przykład tworzy puli adresów zaplecza, o nazwie *myBackEndPool*:</span><span class="sxs-lookup"><span data-stu-id="959f0-137">The following example creates a backend address pool named *myBackEndPool*:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="959f0-138">Teraz Utwórz moduł równoważenia obciążenia z [AzureRmLoadBalancer nowy](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="959f0-138">Now, create the load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="959f0-139">Poniższy przykład tworzy moduł równoważenia obciążenia o nazwie *myLoadBalancer* przy użyciu *myPublicIP* adres:</span><span class="sxs-lookup"><span data-stu-id="959f0-139">The following example creates a load balancer named *myLoadBalancer* using the *myPublicIP* address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a><span data-ttu-id="959f0-140">Utworzyć sondy kondycji</span><span class="sxs-lookup"><span data-stu-id="959f0-140">Create a health probe</span></span>
<span data-ttu-id="959f0-141">Aby zezwolić usłudze równoważenia obciążenia do monitorowania stanu aplikacji, należy użyć sondy kondycji.</span><span class="sxs-lookup"><span data-stu-id="959f0-141">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="959f0-142">Sondy kondycji dynamicznie dodaje lub usuwa maszyn wirtualnych z oparte na ich odpowiedzi na sprawdzenie kondycji obrót usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="959f0-142">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="959f0-143">Domyślnie maszyny Wirtualnej zostanie usunięte z dystrybucji modułu równoważenia obciążenia po dwóch kolejnych błędów na 15 sekund.</span><span class="sxs-lookup"><span data-stu-id="959f0-143">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="959f0-144">Można utworzyć sondy kondycji, na podstawie protokołu lub stronę wyboru kondycji określonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="959f0-144">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="959f0-145">Poniższy przykład tworzy sondowaniem TCP.</span><span class="sxs-lookup"><span data-stu-id="959f0-145">The following example creates a TCP probe.</span></span> <span data-ttu-id="959f0-146">Można również utworzyć niestandardowe sond HTTP więcej kontroli kondycji szczegółowe.</span><span class="sxs-lookup"><span data-stu-id="959f0-146">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="959f0-147">Podczas korzystania z niestandardowego badanie HTTP, należy utworzyć strona sprawdzania kondycji, takich jak *healthcheck.aspx*.</span><span class="sxs-lookup"><span data-stu-id="959f0-147">When using a custom HTTP probe, you must create the health check page, such as *healthcheck.aspx*.</span></span> <span data-ttu-id="959f0-148">Sonda musi zwracać **HTTP 200 OK** odpowiedzi dla usługi równoważenia obciążenia zachować hosta w obrotu.</span><span class="sxs-lookup"><span data-stu-id="959f0-148">The probe must return an **HTTP 200 OK** response for the load balancer to keep the host in rotation.</span></span>

<span data-ttu-id="959f0-149">Aby utworzyć sondy kondycji TCP, należy użyć [AzureRmLoadBalancerProbeConfig Dodaj](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="959f0-149">To create a TCP health probe, you use [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="959f0-150">Poniższy przykład tworzy badanie kondycji o nazwie *myHealthProbe* który monitoruje każdej maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="959f0-150">The following example creates a health probe named *myHealthProbe* that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

<span data-ttu-id="959f0-151">Aktualizacja usługi równoważenia obciążenia z [AzureRmLoadBalancer zestaw](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="959f0-151">Update the load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="959f0-152">Tworzenie reguły modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="959f0-152">Create a load balancer rule</span></span>
<span data-ttu-id="959f0-153">Reguły modułu równoważenia obciążenia jest używany do definiowania rozkład ruchu do maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="959f0-153">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span> <span data-ttu-id="959f0-154">Należy zdefiniować konfiguracji IP frontonu dla ruchu przychodzącego i puli adresów IP zaplecza, aby odbierać ruch, wraz z wymagany port źródłowy i docelowy.</span><span class="sxs-lookup"><span data-stu-id="959f0-154">You define the front-end IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span></span> <span data-ttu-id="959f0-155">Aby upewnij się, że tylko dobrej kondycji maszyn wirtualnych odbieranie ruchu, również zdefiniować sondy kondycji do użycia.</span><span class="sxs-lookup"><span data-stu-id="959f0-155">To make sure only healthy VMs receive traffic, you also define the health probe to use.</span></span>

<span data-ttu-id="959f0-156">Tworzenie reguły modułu równoważenia obciążenia z [AzureRmLoadBalancerRuleConfig Dodaj](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="959f0-156">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="959f0-157">Poniższy przykład tworzy regułę równoważenia obciążenia o nazwie *myLoadBalancerRule* i równoważy ruch na porcie *80*:</span><span class="sxs-lookup"><span data-stu-id="959f0-157">The following example creates a load balancer rule named *myLoadBalancerRule* and balances traffic on port *80*:</span></span>

```powershell
$probe = Get-AzureRmLoadBalancerProbeConfig -LoadBalancer $lb -Name myHealthProbe

Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80 `
  -Probe $probe
```

<span data-ttu-id="959f0-158">Aktualizacja usługi równoważenia obciążenia z [AzureRmLoadBalancer zestaw](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="959f0-158">Update the load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a><span data-ttu-id="959f0-159">Skonfiguruj sieć wirtualną</span><span class="sxs-lookup"><span data-stu-id="959f0-159">Configure virtual network</span></span>
<span data-ttu-id="959f0-160">Przed wdrożeniem niektórych maszyn wirtualnych i przetestować z usługi równoważenia, Utwórz pomocnicze zasoby sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="959f0-160">Before you deploy some VMs and can test your balancer, create the supporting virtual network resources.</span></span> <span data-ttu-id="959f0-161">Aby uzyskać więcej informacji o sieciach wirtualnych, zobacz [Zarządzanie sieciami wirtualnymi Azure](tutorial-virtual-network.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="959f0-161">For more information about virtual networks, see the [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="959f0-162">Utwórz zasoby sieciowe</span><span class="sxs-lookup"><span data-stu-id="959f0-162">Create network resources</span></span>
<span data-ttu-id="959f0-163">Tworzenie sieci wirtualnej z [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="959f0-163">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="959f0-164">Poniższy przykład tworzy sieć wirtualną o nazwie *myVnet* z *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="959f0-164">The following example creates a virtual network named *myVnet* with *mySubnet*:</span></span>

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create the virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

<span data-ttu-id="959f0-165">Tworzenie reguły grupy zabezpieczeń sieci z [AzureRmNetworkSecurityRuleConfig nowy](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), należy utworzyć grupę zabezpieczeń sieci z [AzureRmNetworkSecurityGroup nowy](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="959f0-165">Create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), then create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="959f0-166">Dodaj sieciową grupę zabezpieczeń do podsieci o [AzureRmVirtualNetworkSubnetConfig zestaw](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) , a następnie zaktualizować sieci wirtualnej z [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="959f0-166">Add the network security group to the subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) and then update the virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span></span> 

<span data-ttu-id="959f0-167">Poniższy przykład tworzy regułę grupy zabezpieczeń sieci o nazwie *myNetworkSecurityGroup* i stosuje je do *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="959f0-167">The following example creates a network security group rule named *myNetworkSecurityGroup* and applies it to *mySubnet*:</span></span>

```powershell
# Create security rule config
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

# Create the network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply the network security group to a subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update the virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

<span data-ttu-id="959f0-168">Wirtualne karty sieciowe są tworzone za pomocą [AzureRmNetworkInterface nowy](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="959f0-168">Virtual NICs are created with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="959f0-169">Poniższy przykład tworzy trzy wirtualne karty sieciowe.</span><span class="sxs-lookup"><span data-stu-id="959f0-169">The following example creates three virtual NICs.</span></span> <span data-ttu-id="959f0-170">(Jedną wirtualną kartę Sieciową dla każdej maszyny Wirtualnej można utworzyć dla aplikacji w poniższych krokach).</span><span class="sxs-lookup"><span data-stu-id="959f0-170">(One virtual NIC for each VM you create for your app in the following steps).</span></span> <span data-ttu-id="959f0-171">Można utworzyć dodatkowe wirtualne karty sieciowe i maszyn wirtualnych w dowolnym momencie i dodaj je do usługi równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="959f0-171">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -Name myNic$i `
     -Location EastUS `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}
```

## <a name="create-virtual-machines"></a><span data-ttu-id="959f0-172">Tworzenie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="959f0-172">Create virtual machines</span></span>
<span data-ttu-id="959f0-173">Aby zwiększyć wysoką dostępność aplikacji, umieść maszyn wirtualnych w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="959f0-173">To improve the high availability of your app, place your VMs in an availability set.</span></span>

<span data-ttu-id="959f0-174">Utwórz zestaw o dostępności [AzureRmAvailabilitySet nowy](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="959f0-174">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="959f0-175">Poniższy przykład tworzy zbiór nazwanego dostępności *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="959f0-175">The following example creates an availability set named *myAvailabilitySet*:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

<span data-ttu-id="959f0-176">Ustaw nazwę użytkownika i hasło administratora dla maszyn wirtualnych o [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="959f0-176">Set an administrator username and password for the VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="959f0-177">Teraz można tworzyć maszyn wirtualnych o [AzureRmVM nowy](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="959f0-177">Now you can create the VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="959f0-178">Poniższy przykład tworzy trzech maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="959f0-178">The following example creates three VMs:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
  $vm = New-AzureRmVMConfig `
    -VMName myVM$i `
    -VMSize Standard_D1 `
    -AvailabilitySetId $availabilitySet.Id
  $vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM$i `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
  $vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
  $vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk$i `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
  $nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic$i
  $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
  New-AzureRmVM `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Location EastUS `
    -VM $vm
}
```

<span data-ttu-id="959f0-179">Trwa kilka minut, aby utworzyć i skonfigurować wszystkie trzy maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="959f0-179">It takes a few minutes to create and configure all three VMs.</span></span>

### <a name="install-iis-with-custom-script-extension"></a><span data-ttu-id="959f0-180">Instalowanie usług IIS przy użyciu niestandardowego rozszerzenia skryptu</span><span class="sxs-lookup"><span data-stu-id="959f0-180">Install IIS with Custom Script Extension</span></span>
<span data-ttu-id="959f0-181">W poprzednich samouczek dotyczący [sposobu dostosowywania maszyny wirtualnej systemu Windows](tutorial-automate-vm-deployment.md), wiesz, jak można zautomatyzować dostosowania maszyny Wirtualnej z niestandardowego skryptu rozszerzenia dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="959f0-181">In a previous tutorial on [How to customize a Windows virtual machine](tutorial-automate-vm-deployment.md), you learned how to automate VM customization with the Custom Script Extension for Windows.</span></span> <span data-ttu-id="959f0-182">Te same podejście służy do instalowania i konfigurowania usług IIS na maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="959f0-182">You can use the same approach to install and configure IIS on your VMs.</span></span>

<span data-ttu-id="959f0-183">Użyj [AzureRmVMExtension zestaw](/powershell/module/azurerm.compute/set-azurermvmextension) do zainstalowania niestandardowe rozszerzenie skryptu.</span><span class="sxs-lookup"><span data-stu-id="959f0-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) to install the Custom Script Extension.</span></span> <span data-ttu-id="959f0-184">Uruchamia rozszerzenia `powershell Add-WindowsFeature Web-Server` Aby zainstalować serwer sieci Web usług IIS, a następnie aktualizacje *Default.htm* stronę, aby wyświetlić nazwę hosta maszyny wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="959f0-184">The extension runs `powershell Add-WindowsFeature Web-Server` to install the IIS webserver and then updates the *Default.htm* page to show the hostname of the VM:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
     -Location EastUS
}
```

## <a name="test-load-balancer"></a><span data-ttu-id="959f0-185">Test usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="959f0-185">Test load balancer</span></span>
<span data-ttu-id="959f0-186">Publiczny adres IP z usługi równoważenia obciążenia z [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="959f0-186">Obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="959f0-187">Poniższy przykład uzyskuje adres IP dla *myPublicIP* utworzony wcześniej:</span><span class="sxs-lookup"><span data-stu-id="959f0-187">The following example obtains the IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

<span data-ttu-id="959f0-188">Następnie można wprowadzić publicznego adresu IP w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="959f0-188">You can then enter the public IP address in to a web browser.</span></span> <span data-ttu-id="959f0-189">Witryna sieci Web jest wyświetlany, łącznie z nazwą hosta maszyny Wirtualnej dystrybuowanej usługi równoważenia obciążenia w ruchu, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="959f0-189">The website is displayed, including the hostname of the VM that the load balancer distributed traffic to as in the following example:</span></span>

![Witryna sieci Web IIS uruchomiona](./media/tutorial-load-balancer/running-iis-website.png)

<span data-ttu-id="959f0-191">Aby wyświetlić Dystrybuuj ruch we wszystkich trzech maszyn wirtualnych z tą aplikacją usługi równoważenia obciążenia, możesz można życie odświeżania przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="959f0-191">To see the load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="959f0-192">Dodawanie i usuwanie maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="959f0-192">Add and remove VMs</span></span>
<span data-ttu-id="959f0-193">Może być konieczne przeprowadzenie konserwacji na maszynach wirtualnych z tą aplikacją, takich jak instalowanie aktualizacji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="959f0-193">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="959f0-194">Aby poradzić sobie z zwiększenie obciążenia do aplikacji, może być konieczne dodanie kolejnych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="959f0-194">To deal with increased traffic to your app, you may need to add additional VMs.</span></span> <span data-ttu-id="959f0-195">W tej sekcji przedstawiono sposób Usuń lub Dodaj Maszynę wirtualną z modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="959f0-195">This section shows you how to remove or add a VM from the load balancer.</span></span>

### <a name="remove-a-vm-from-the-load-balancer"></a><span data-ttu-id="959f0-196">Usuń Maszynę wirtualną z usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="959f0-196">Remove a VM from the load balancer</span></span>
<span data-ttu-id="959f0-197">Pobierz karty interfejsu sieciowego z [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), a następnie ustaw *Loadbalancerbackendaddresspool* właściwość wirtualnej karty Sieciowej *$null*.</span><span class="sxs-lookup"><span data-stu-id="959f0-197">Get the network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), then set the *LoadBalancerBackendAddressPools* property of the virtual NIC to *$null*.</span></span> <span data-ttu-id="959f0-198">Na koniec zaktualizuj wirtualnych kart sieciowych.:</span><span class="sxs-lookup"><span data-stu-id="959f0-198">Finally, update the virtual NIC.:</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="959f0-199">Aby wyświetlić rozpowszechniają ruchu pozostałych dwóch maszyn wirtualnych z tą aplikacją usługi równoważenia obciążenia można można życie odświeżania przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="959f0-199">To see the load balancer distribute traffic across the remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="959f0-200">Teraz można przeprowadzać konserwacji na maszynie Wirtualnej, takie jak instalowanie aktualizacji systemu operacyjnego lub wykonywania ponownego uruchomienia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="959f0-200">You can now perform maintenance on the VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-to-the-load-balancer"></a><span data-ttu-id="959f0-201">Dodaj Maszynę wirtualną z usługą równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="959f0-201">Add a VM to the load balancer</span></span>
<span data-ttu-id="959f0-202">Po konserwacja maszyny Wirtualnej, lub jeśli trzeba zwiększyć wydajność, ustaw *Loadbalancerbackendaddresspool* właściwość wirtualnej karty Sieciowej *BackendAddressPool* z [ Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="959f0-202">After performing VM maintenance, or if you need to expand capacity, set the *LoadBalancerBackendAddressPools* property of the virtual NIC to the *BackendAddressPool* from [Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span></span>

<span data-ttu-id="959f0-203">Pobierz moduł równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="959f0-203">Get the load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="959f0-204">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="959f0-204">Next steps</span></span>

<span data-ttu-id="959f0-205">W tym samouczku utworzony moduł równoważenia obciążenia i dołączone do maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="959f0-205">In this tutorial, you created a load balancer and attached VMs to it.</span></span> <span data-ttu-id="959f0-206">Możesz przedstawiono sposób do:</span><span class="sxs-lookup"><span data-stu-id="959f0-206">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="959f0-207">Tworzenie usługi równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="959f0-207">Create an Azure load balancer</span></span>
> * <span data-ttu-id="959f0-208">Utwórz kondycji sondę modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="959f0-208">Create a load balancer health probe</span></span>
> * <span data-ttu-id="959f0-209">Tworzenie reguły ruchu usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="959f0-209">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="959f0-210">Niestandardowe rozszerzenie skryptu umożliwiają utworzenie podstawowej witryny usług IIS</span><span class="sxs-lookup"><span data-stu-id="959f0-210">Use the Custom Script Extension to create a basic IIS site</span></span>
> * <span data-ttu-id="959f0-211">Tworzenie maszyn wirtualnych i dołączanie do usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="959f0-211">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="959f0-212">Wyświetl modułu równoważenia obciążenia w akcji</span><span class="sxs-lookup"><span data-stu-id="959f0-212">View a load balancer in action</span></span>
> * <span data-ttu-id="959f0-213">Dodawanie i usuwanie maszyny wirtualne z modułem równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="959f0-213">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="959f0-214">Przejście do następnym samouczku, aby dowiedzieć się, jak zarządzać sieci maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="959f0-214">Advance to the next tutorial to learn how to manage VM networking.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="959f0-215">Zarządzanie maszynami wirtualnymi i sieciami wirtualnymi</span><span class="sxs-lookup"><span data-stu-id="959f0-215">Manage VMs and virtual networks</span></span>](./tutorial-virtual-network.md)
