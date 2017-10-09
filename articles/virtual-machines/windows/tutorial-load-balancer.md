---
title: aaaHow tooload saldo maszyn wirtualnych systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse hello Azure obciążenia toocreate równoważenia aplikacji wysokiej dostępności i bezpieczne w trzech maszyn wirtualnych systemu Windows"
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
ms.openlocfilehash: bfbd6a24e90a33e60d7d4f7b0c471af5d4e71f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-windows-virtual-machines-in-azure-toocreate-a-highly-available-application"></a><span data-ttu-id="e7edc-103">Jak tooload saldo maszyny wirtualne systemu Windows Azure toocreate wysokiej dostępności aplikacji</span><span class="sxs-lookup"><span data-stu-id="e7edc-103">How tooload balance Windows virtual machines in Azure toocreate a highly available application</span></span>
<span data-ttu-id="e7edc-104">Równoważenie obciążenia sieciowego zapewnia wyższy poziom dostępności dzięki rozproszeniu przychodzące żądania między wieloma maszynami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="e7edc-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="e7edc-105">Z tego samouczka dowiesz się o hello różnych składników usługi równoważenia obciążenia Azure hello dystrybucji ruchu, które zapewniają wysoką dostępność.</span><span class="sxs-lookup"><span data-stu-id="e7edc-105">In this tutorial, you learn about hello different components of hello Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="e7edc-106">Omawiane kwestie:</span><span class="sxs-lookup"><span data-stu-id="e7edc-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e7edc-107">Tworzenie usługi równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="e7edc-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="e7edc-108">Utwórz kondycji sondę modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="e7edc-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="e7edc-109">Tworzenie reguły ruchu usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="e7edc-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="e7edc-110">Użyj hello niestandardowe rozszerzenie skryptu toocreate podstawowej witryny usług IIS</span><span class="sxs-lookup"><span data-stu-id="e7edc-110">Use hello Custom Script Extension toocreate a basic IIS site</span></span>
> * <span data-ttu-id="e7edc-111">Tworzenie maszyn wirtualnych i Dołącz tooa modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="e7edc-111">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="e7edc-112">Wyświetl modułu równoważenia obciążenia w akcji</span><span class="sxs-lookup"><span data-stu-id="e7edc-112">View a load balancer in action</span></span>
> * <span data-ttu-id="e7edc-113">Dodawanie i usuwanie maszyny wirtualne z modułem równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="e7edc-113">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="e7edc-114">Ten samouczek wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="e7edc-114">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="e7edc-115">Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="e7edc-115">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="e7edc-116">Jeśli potrzebujesz tooupgrade, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="e7edc-116">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="azure-load-balancer-overview"></a><span data-ttu-id="e7edc-117">Omówienie usługi równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="e7edc-117">Azure load balancer overview</span></span>
<span data-ttu-id="e7edc-118">Moduł równoważenia obciążenia Azure jest równoważenia obciążenia warstwy 4 (TCP, UDP), który zapewnia wysoką dostępność, przekazując przychodzący ruch między maszynami wirtualnymi w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="e7edc-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="e7edc-119">Kondycji sondę modułu równoważenia obciążenia monitoruje danego portu na każdej maszynie Wirtualnej, a tylko dystrybuuje ruch tooan operacyjne maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e7edc-119">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

<span data-ttu-id="e7edc-120">Należy zdefiniować frontonu konfiguracji adresu IP, który zawiera co najmniej jeden publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="e7edc-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="e7edc-121">Ta konfiguracja frontonu IP umożliwia toobe, a aplikacje usługi równoważenia obciążenia dostępny za pośrednictwem hello Internet.</span><span class="sxs-lookup"><span data-stu-id="e7edc-121">This front-end IP configuration allows your load balancer and applications toobe accessible over hello Internet.</span></span> 

<span data-ttu-id="e7edc-122">Maszyny wirtualne połączenie usługi równoważenia obciążenia tooa przy użyciu ich karty interfejsu sieci wirtualnej (NIC).</span><span class="sxs-lookup"><span data-stu-id="e7edc-122">Virtual machines connect tooa load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="e7edc-123">toodistribute toohello ruch maszyn wirtualnych, puli adresów zaplecza zawiera adresy IP hello hello wirtualnych (NIC) toohello podłączonej usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e7edc-123">toodistribute traffic toohello VMs, a back-end address pool contains hello IP addresses of hello virtual (NICs) connected toohello load balancer.</span></span>

<span data-ttu-id="e7edc-124">toocontrol hello przepływu ruchu, należy zdefiniować reguły modułu równoważenia obciążenia dla określonych portów i protokołów, które mapują tooyour maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e7edc-124">toocontrol hello flow of traffic, you define load balancer rules for specific ports and protocols that map tooyour VMs.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="e7edc-125">Tworzenie usługi równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="e7edc-125">Create Azure load balancer</span></span>
<span data-ttu-id="e7edc-126">W tej sekcji Szczegóły, jak można tworzyć i konfigurować poszczególnych składników usługi równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="e7edc-126">This section details how you can create and configure each component of hello load balancer.</span></span> <span data-ttu-id="e7edc-127">Przed utworzeniem przez moduł równoważenia obciążenia, Utwórz nową grupę zasobów o [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="e7edc-127">Before you can create your load balancer, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="e7edc-128">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupLoadBalancer* w hello *EastUS* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="e7edc-128">hello following example creates a resource group named *myResourceGroupLoadBalancer* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="e7edc-129">Tworzenie publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="e7edc-129">Create a public IP address</span></span>
<span data-ttu-id="e7edc-130">tooaccess aplikacji na hello Internet, należy publicznego adresu IP dla modułu równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="e7edc-130">tooaccess your app on hello Internet, you need a public IP address for hello load balancer.</span></span> <span data-ttu-id="e7edc-131">Utwórz publiczny adres IP z [AzureRmPublicIpAddress nowy](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="e7edc-131">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="e7edc-132">Witaj poniższy przykład tworzy publiczny adres IP o nazwie *myPublicIP* w hello *myResourceGroupLoadBalancer* grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="e7edc-132">hello following example creates a public IP address named *myPublicIP* in hello *myResourceGroupLoadBalancer* resource group:</span></span>

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="e7edc-133">Tworzenie modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="e7edc-133">Create a load balancer</span></span>
<span data-ttu-id="e7edc-134">Utwórz na adres IP frontonu [AzureRmLoadBalancerFrontendIpConfig nowy](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="e7edc-134">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="e7edc-135">Witaj poniższy przykład tworzy adresu IP serwera sieci Web o nazwie *myFrontEndPool*:</span><span class="sxs-lookup"><span data-stu-id="e7edc-135">hello following example creates a frontend IP address named *myFrontEndPool*:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

<span data-ttu-id="e7edc-136">Utwórz pulę adresów zaplecza z [AzureRmLoadBalancerBackendAddressPoolConfig nowy](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="e7edc-136">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="e7edc-137">Witaj poniższy przykład tworzy puli adresów zaplecza, o nazwie *myBackEndPool*:</span><span class="sxs-lookup"><span data-stu-id="e7edc-137">hello following example creates a backend address pool named *myBackEndPool*:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="e7edc-138">Teraz utworzymy hello modułu równoważenia obciążenia z [AzureRmLoadBalancer nowy](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="e7edc-138">Now, create hello load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="e7edc-139">Witaj poniższy przykład tworzy moduł równoważenia obciążenia o nazwie *myLoadBalancer* przy użyciu hello *myPublicIP* adres:</span><span class="sxs-lookup"><span data-stu-id="e7edc-139">hello following example creates a load balancer named *myLoadBalancer* using hello *myPublicIP* address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a><span data-ttu-id="e7edc-140">Utworzyć sondy kondycji</span><span class="sxs-lookup"><span data-stu-id="e7edc-140">Create a health probe</span></span>
<span data-ttu-id="e7edc-141">tooallow hello stanu usługi równoważenia obciążenia toomonitor hello aplikacji, możesz użyć sondy kondycji.</span><span class="sxs-lookup"><span data-stu-id="e7edc-141">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="e7edc-142">sondy kondycji Hello dynamicznie dodaje lub usuwa maszyn wirtualnych z obrotu usługi równoważenia obciążenia hello oparte na ich kontroli toohealth odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="e7edc-142">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="e7edc-143">Domyślnie maszyny Wirtualnej zostanie usunięte z dystrybucji modułu równoważenia obciążenia powitania po dwóch kolejnych błędów na 15 sekund.</span><span class="sxs-lookup"><span data-stu-id="e7edc-143">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="e7edc-144">Można utworzyć sondy kondycji, na podstawie protokołu lub stronę wyboru kondycji określonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e7edc-144">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="e7edc-145">Witaj poniższy przykład tworzy badanie TCP.</span><span class="sxs-lookup"><span data-stu-id="e7edc-145">hello following example creates a TCP probe.</span></span> <span data-ttu-id="e7edc-146">Można również utworzyć niestandardowe sond HTTP więcej kontroli kondycji szczegółowe.</span><span class="sxs-lookup"><span data-stu-id="e7edc-146">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="e7edc-147">Podczas korzystania z niestandardowego badanie HTTP, należy utworzyć hello strona sprawdzania kondycji, takich jak *healthcheck.aspx*.</span><span class="sxs-lookup"><span data-stu-id="e7edc-147">When using a custom HTTP probe, you must create hello health check page, such as *healthcheck.aspx*.</span></span> <span data-ttu-id="e7edc-148">Sonda Hello musi zwracać **HTTP 200 OK** odpowiedzi dla hosta usługi równoważenia obciążenia hello hello tookeep rotacji.</span><span class="sxs-lookup"><span data-stu-id="e7edc-148">hello probe must return an **HTTP 200 OK** response for hello load balancer tookeep hello host in rotation.</span></span>

<span data-ttu-id="e7edc-149">Użyj toocreate sondy kondycji TCP [AzureRmLoadBalancerProbeConfig Dodaj](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="e7edc-149">toocreate a TCP health probe, you use [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="e7edc-150">Witaj poniższy przykład tworzy badanie kondycji o nazwie *myHealthProbe* który monitoruje każdej maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="e7edc-150">hello following example creates a health probe named *myHealthProbe* that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

<span data-ttu-id="e7edc-151">Zaktualizuj hello modułu równoważenia obciążenia z [AzureRmLoadBalancer zestaw](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="e7edc-151">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="e7edc-152">Tworzenie reguły modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="e7edc-152">Create a load balancer rule</span></span>
<span data-ttu-id="e7edc-153">Reguły modułu równoważenia obciążenia jest używany toodefine sposób ruch jest rozproszonej toohello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e7edc-153">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span> <span data-ttu-id="e7edc-154">Należy zdefiniować hello frontonu konfigurację adresu IP dla ruchu przychodzącego hello i hello zaplecza IP puli tooreceive hello ruchu, wraz z hello wymagane źródłowy i port docelowy.</span><span class="sxs-lookup"><span data-stu-id="e7edc-154">You define hello front-end IP configuration for hello incoming traffic and hello back-end IP pool tooreceive hello traffic, along with hello required source and destination port.</span></span> <span data-ttu-id="e7edc-155">toomake się, że tylko dobrej kondycji maszyn wirtualnych odbieranie ruchu, możesz również definiować toouse sondy kondycji hello.</span><span class="sxs-lookup"><span data-stu-id="e7edc-155">toomake sure only healthy VMs receive traffic, you also define hello health probe toouse.</span></span>

<span data-ttu-id="e7edc-156">Tworzenie reguły modułu równoważenia obciążenia z [AzureRmLoadBalancerRuleConfig Dodaj](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="e7edc-156">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="e7edc-157">Witaj poniższy przykład tworzy regułę równoważenia obciążenia o nazwie *myLoadBalancerRule* i równoważy ruch na porcie *80*:</span><span class="sxs-lookup"><span data-stu-id="e7edc-157">hello following example creates a load balancer rule named *myLoadBalancerRule* and balances traffic on port *80*:</span></span>

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

<span data-ttu-id="e7edc-158">Zaktualizuj hello modułu równoważenia obciążenia z [AzureRmLoadBalancer zestaw](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="e7edc-158">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a><span data-ttu-id="e7edc-159">Konfigurowanie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e7edc-159">Configure virtual network</span></span>
<span data-ttu-id="e7edc-160">Przed wdrożeniem niektórych maszyn wirtualnych i przetestować z usługi równoważenia, Utwórz hello obsługi zasobów sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e7edc-160">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="e7edc-161">Aby uzyskać więcej informacji o sieciach wirtualnych, zobacz hello [Zarządzanie sieciami wirtualnymi Azure](tutorial-virtual-network.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="e7edc-161">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="e7edc-162">Utwórz zasoby sieciowe</span><span class="sxs-lookup"><span data-stu-id="e7edc-162">Create network resources</span></span>
<span data-ttu-id="e7edc-163">Tworzenie sieci wirtualnej z [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="e7edc-163">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="e7edc-164">Witaj poniższy przykład tworzy sieć wirtualną o nazwie *myVnet* z *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="e7edc-164">hello following example creates a virtual network named *myVnet* with *mySubnet*:</span></span>

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create hello virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

<span data-ttu-id="e7edc-165">Tworzenie reguły grupy zabezpieczeń sieci z [AzureRmNetworkSecurityRuleConfig nowy](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), należy utworzyć grupę zabezpieczeń sieci z [AzureRmNetworkSecurityGroup nowy](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="e7edc-165">Create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), then create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="e7edc-166">Dodaj podsieć toohello grupy zabezpieczeń sieci hello z [AzureRmVirtualNetworkSubnetConfig zestaw](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) , a następnie zaktualizować sieci wirtualnej hello o [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="e7edc-166">Add hello network security group toohello subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) and then update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span></span> 

<span data-ttu-id="e7edc-167">Witaj poniższy przykład tworzy regułę grupy zabezpieczeń sieci o nazwie *myNetworkSecurityGroup* i stosuje je zbyt*mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="e7edc-167">hello following example creates a network security group rule named *myNetworkSecurityGroup* and applies it too*mySubnet*:</span></span>

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

# Create hello network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply hello network security group tooa subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update hello virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

<span data-ttu-id="e7edc-168">Wirtualne karty sieciowe są tworzone za pomocą [AzureRmNetworkInterface nowy](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="e7edc-168">Virtual NICs are created with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="e7edc-169">Witaj poniższy przykład tworzy trzy wirtualne karty sieciowe.</span><span class="sxs-lookup"><span data-stu-id="e7edc-169">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="e7edc-170">(Jedną wirtualną kartę Sieciową dla każdej maszyny Wirtualnej można utworzyć dla aplikacji w hello następujące kroki).</span><span class="sxs-lookup"><span data-stu-id="e7edc-170">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="e7edc-171">Można tworzyć dodatkowe wirtualne karty sieciowe i maszyn wirtualnych w dowolnym momencie i dodać je toohello usługi równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="e7edc-171">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

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

## <a name="create-virtual-machines"></a><span data-ttu-id="e7edc-172">Tworzenie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="e7edc-172">Create virtual machines</span></span>
<span data-ttu-id="e7edc-173">tooimprove hello wysoką dostępność aplikacji, umieść maszyn wirtualnych w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="e7edc-173">tooimprove hello high availability of your app, place your VMs in an availability set.</span></span>

<span data-ttu-id="e7edc-174">Utwórz zestaw o dostępności [AzureRmAvailabilitySet nowy](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="e7edc-174">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="e7edc-175">Witaj poniższy przykład tworzy zbiór nazwanego dostępności *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="e7edc-175">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

<span data-ttu-id="e7edc-176">Ustaw nazwę użytkownika i hasło administratora dla maszyn wirtualnych hello z [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="e7edc-176">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="e7edc-177">Teraz można tworzyć maszyn wirtualnych hello o [AzureRmVM nowy](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="e7edc-177">Now you can create hello VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="e7edc-178">Witaj poniższy przykład tworzy trzech maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="e7edc-178">hello following example creates three VMs:</span></span>

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

<span data-ttu-id="e7edc-179">Go zajmuje kilka minut toocreate i skonfiguruj wszystkie trzy maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="e7edc-179">It takes a few minutes toocreate and configure all three VMs.</span></span>

### <a name="install-iis-with-custom-script-extension"></a><span data-ttu-id="e7edc-180">Instalowanie usług IIS przy użyciu niestandardowego rozszerzenia skryptu</span><span class="sxs-lookup"><span data-stu-id="e7edc-180">Install IIS with Custom Script Extension</span></span>
<span data-ttu-id="e7edc-181">W poprzednich samouczek dotyczący [jak toocustomize maszyny wirtualnej systemu Windows](tutorial-automate-vm-deployment.md), wiesz, jak tooautomate dostosowywania maszyny Wirtualnej z hello niestandardowe rozszerzenie skryptu systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="e7edc-181">In a previous tutorial on [How toocustomize a Windows virtual machine](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with hello Custom Script Extension for Windows.</span></span> <span data-ttu-id="e7edc-182">Można użyć hello sam podejścia tooinstall i skonfigurowanie usług IIS na maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="e7edc-182">You can use hello same approach tooinstall and configure IIS on your VMs.</span></span>

<span data-ttu-id="e7edc-183">Użyj [AzureRmVMExtension zestaw](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello niestandardowe rozszerzenie skryptu.</span><span class="sxs-lookup"><span data-stu-id="e7edc-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Custom Script Extension.</span></span> <span data-ttu-id="e7edc-184">Witaj uruchamia rozszerzenia `powershell Add-WindowsFeature Web-Server` tooinstall hello serwer sieci Web usług IIS, a następnie aktualizacje hello *Default.htm* strony tooshow hello nazwy hosta hello maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="e7edc-184">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver and then updates hello *Default.htm* page tooshow hello hostname of hello VM:</span></span>

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

## <a name="test-load-balancer"></a><span data-ttu-id="e7edc-185">Test usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="e7edc-185">Test load balancer</span></span>
<span data-ttu-id="e7edc-186">Uzyskaj hello publicznego adresu IP z usługi równoważenia obciążenia z [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="e7edc-186">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="e7edc-187">Witaj poniższy przykład uzyskuje hello adres IP dla *myPublicIP* utworzony wcześniej:</span><span class="sxs-lookup"><span data-stu-id="e7edc-187">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

<span data-ttu-id="e7edc-188">W przeglądarce sieci web tooa można następnie wprowadzić hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="e7edc-188">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="e7edc-189">Hello witryny sieci Web jest wyświetlany, łącznie z nazwą hosta hello hello maszyny Wirtualnej tego modułu równoważenia obciążenia hello rozproszonych tooas ruchu w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="e7edc-189">hello website is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Witryna sieci Web IIS uruchomiona](./media/tutorial-load-balancer/running-iis-website.png)

<span data-ttu-id="e7edc-191">Moduł równoważenia obciążenia hello toosee Dystrybuuj ruch we wszystkich trzech maszyn wirtualnych z tą aplikacją, użytkownik może życie odświeżania przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="e7edc-191">toosee hello load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="e7edc-192">Dodawanie i usuwanie maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="e7edc-192">Add and remove VMs</span></span>
<span data-ttu-id="e7edc-193">Może być konieczne tooperform konserwacji na powitania maszyn wirtualnych z tą aplikacją, takich jak instalowanie aktualizacji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="e7edc-193">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="e7edc-194">toodeal z aplikacją tooyour zwiększenie obciążenia, może być konieczne tooadd kolejnych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e7edc-194">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="e7edc-195">W tej sekcji opisano sposób tooremove lub dodać maszyny Wirtualnej z hello modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e7edc-195">This section shows you how tooremove or add a VM from hello load balancer.</span></span>

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="e7edc-196">Usuń Maszynę wirtualną z hello modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="e7edc-196">Remove a VM from hello load balancer</span></span>
<span data-ttu-id="e7edc-197">Pobierz hello karty interfejsu sieciowego z [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), następnie zestaw hello *Loadbalancerbackendaddresspool* właściwość hello wirtualnej karty Sieciowej, za*$null*.</span><span class="sxs-lookup"><span data-stu-id="e7edc-197">Get hello network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), then set hello *LoadBalancerBackendAddressPools* property of hello virtual NIC too*$null*.</span></span> <span data-ttu-id="e7edc-198">Na koniec zaktualizuj hello wirtualnych kart sieciowych.:</span><span class="sxs-lookup"><span data-stu-id="e7edc-198">Finally, update hello virtual NIC.:</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="e7edc-199">Moduł równoważenia obciążenia hello toosee rozpowszechniają ruchu hello dwóch pozostałych maszyn wirtualnych z tą aplikacją możesz można życie odświeżania przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="e7edc-199">toosee hello load balancer distribute traffic across hello remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="e7edc-200">Teraz można przeprowadzać konserwacji na powitania maszynę Wirtualną, takie jak instalowanie aktualizacji systemu operacyjnego lub wykonywania ponownego uruchomienia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e7edc-200">You can now perform maintenance on hello VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="e7edc-201">Dodaj usługi równoważenia obciążenia toohello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e7edc-201">Add a VM toohello load balancer</span></span>
<span data-ttu-id="e7edc-202">Po konserwacja maszyny Wirtualnej lub tooexpand pojemności, należy ustawić hello *Loadbalancerbackendaddresspool* właściwości hello wirtualnej karty Sieciowej toohello *BackendAddressPool* z [ Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="e7edc-202">After performing VM maintenance, or if you need tooexpand capacity, set hello *LoadBalancerBackendAddressPools* property of hello virtual NIC toohello *BackendAddressPool* from [Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span></span>

<span data-ttu-id="e7edc-203">Pobierz hello usługi równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="e7edc-203">Get hello load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="e7edc-204">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e7edc-204">Next steps</span></span>

<span data-ttu-id="e7edc-205">W tym samouczku utworzony moduł równoważenia obciążenia i dołączyć tooit maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e7edc-205">In this tutorial, you created a load balancer and attached VMs tooit.</span></span> <span data-ttu-id="e7edc-206">W tym samouczku omówiono:</span><span class="sxs-lookup"><span data-stu-id="e7edc-206">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e7edc-207">Tworzenie usługi równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="e7edc-207">Create an Azure load balancer</span></span>
> * <span data-ttu-id="e7edc-208">Utwórz kondycji sondę modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="e7edc-208">Create a load balancer health probe</span></span>
> * <span data-ttu-id="e7edc-209">Tworzenie reguły ruchu usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="e7edc-209">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="e7edc-210">Użyj hello niestandardowe rozszerzenie skryptu toocreate podstawowej witryny usług IIS</span><span class="sxs-lookup"><span data-stu-id="e7edc-210">Use hello Custom Script Extension toocreate a basic IIS site</span></span>
> * <span data-ttu-id="e7edc-211">Tworzenie maszyn wirtualnych i Dołącz tooa modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="e7edc-211">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="e7edc-212">Wyświetl modułu równoważenia obciążenia w akcji</span><span class="sxs-lookup"><span data-stu-id="e7edc-212">View a load balancer in action</span></span>
> * <span data-ttu-id="e7edc-213">Dodawanie i usuwanie maszyny wirtualne z modułem równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="e7edc-213">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="e7edc-214">Jak przejść dalej toolearn samouczka toohello toomanage sieci maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e7edc-214">Advance toohello next tutorial toolearn how toomanage VM networking.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e7edc-215">Zarządzanie maszynami wirtualnymi i sieciami wirtualnymi</span><span class="sxs-lookup"><span data-stu-id="e7edc-215">Manage VMs and virtual networks</span></span>](./tutorial-virtual-network.md)
