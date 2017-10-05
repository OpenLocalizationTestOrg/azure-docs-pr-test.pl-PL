---
title: "Tworzenie usługi równoważenia obciążenia Azure internetowych w przypadku adresu IPv6 - PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć internetowy modułu równoważenia obciążenia w przypadku adresu IPv6 przy użyciu programu PowerShell dla Menedżera zasobów"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "Protokół IPv6, usługi równoważenia obciążenia azure, podwójnego stosu, publiczny adres ip, natywnego protokołu ipv6, mobile, iot"
ms.assetid: d4c649e3-84ad-4343-8b6a-0e89f0b9e518
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 9d3cd37d3f2912301904b0a35f6fbc978d173079
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-with-ipv6-using-powershell-for-resource-manager"></a><span data-ttu-id="68a99-104">Rozpocząć tworzenie internetowy modułu równoważenia obciążenia w przypadku adresu IPv6 przy użyciu programu PowerShell dla Menedżera zasobów</span><span class="sxs-lookup"><span data-stu-id="68a99-104">Get started creating an Internet facing load balancer with IPv6 using PowerShell for Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="68a99-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="68a99-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="68a99-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="68a99-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="68a99-107">Szablon</span><span class="sxs-lookup"><span data-stu-id="68a99-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="68a99-108">Usługa Azure Load Balancer to moduł równoważenia obciążenia w warstwie 4 (TCP, UDP).</span><span class="sxs-lookup"><span data-stu-id="68a99-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="68a99-109">Moduł równoważenia obciążenia zapewnia wysoką dostępność, dystrybuując ruch przychodzący w wystąpieniach usług o dobrej kondycji w usługach w chmurze lub na maszynach wirtualnych w zestawie modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="68a99-109">The load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="68a99-110">Usługa Azure Load Balancer może także prezentować te usługi na wielu portach i/lub wielu adresach IP.</span><span class="sxs-lookup"><span data-stu-id="68a99-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="68a99-111">Przykładowy scenariusz wdrażania</span><span class="sxs-lookup"><span data-stu-id="68a99-111">Example deployment scenario</span></span>

<span data-ttu-id="68a99-112">Na poniższym diagramie przedstawiono wdrażany w tym artykule rozwiązania do równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="68a99-112">The following diagram illustrates the load balancing solution being deployed in this article.</span></span>

![Scenariusz modułu równoważenia obciążenia](./media/load-balancer-ipv6-internet-ps/lb-ipv6-scenario.png)

<span data-ttu-id="68a99-114">W tym scenariuszu spowoduje utworzenie następujących zasobów platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="68a99-114">In this scenario you will create the following Azure resources:</span></span>

* <span data-ttu-id="68a99-115">Moduł równoważenia obciążenia internetowy z protokołów IPv4 i IPv6 publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="68a99-115">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="68a99-116">dwie reguły równoważenia do mapowania publiczne adresy VIP prywatnej punkty końcowe obciążenia</span><span class="sxs-lookup"><span data-stu-id="68a99-116">two load balancing rules to map the public VIPs to the private endpoints</span></span>
* <span data-ttu-id="68a99-117">Zestaw dostępności w tym zawiera dwie maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="68a99-117">an Availability Set to that contains the two VMs</span></span>
* <span data-ttu-id="68a99-118">dwóch maszyn wirtualnych (VM)</span><span class="sxs-lookup"><span data-stu-id="68a99-118">two virtual machines (VMs)</span></span>
* <span data-ttu-id="68a99-119">Interfejs sieci wirtualnej, dla każdej maszyny Wirtualnej przy użyciu adresów IPv4 i IPv6 przypisany</span><span class="sxs-lookup"><span data-stu-id="68a99-119">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>

## <a name="deploying-the-solution-using-the-azure-powershell"></a><span data-ttu-id="68a99-120">Wdrażanie rozwiązania przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="68a99-120">Deploying the solution using the Azure PowerShell</span></span>

<span data-ttu-id="68a99-121">Poniższe kroki pokazują, jak utworzyć internetowy modułu równoważenia obciążenia przy użyciu usługi Azure Resource Manager przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68a99-121">The following steps show how to create an Internet facing load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="68a99-122">Usługi Azure Resource Manager każdy zasób jest tworzony i skonfigurować osobno, następnie put ze sobą w celu utworzenia zasobu.</span><span class="sxs-lookup"><span data-stu-id="68a99-122">With Azure Resource Manager, each resource is created and configured individually, then put together to create a resource.</span></span>

<span data-ttu-id="68a99-123">Aby wdrożyć usługę równoważenia obciążenia, możesz utworzyć i skonfigurować następujące obiekty:</span><span class="sxs-lookup"><span data-stu-id="68a99-123">To deploy a load balancer, you create and configure the following objects:</span></span>

* <span data-ttu-id="68a99-124">Konfiguracja IP frontonu — publiczne adresy IP dla przychodzącego ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="68a99-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="68a99-125">Pula adresów zaplecza — interfejsy sieciowe (NIC) maszyn wirtualnych odbierających ruch sieciowy z modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="68a99-125">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="68a99-126">Reguły równoważenia obciążenia — reguły mapowania portu publicznego modułu równoważenia obciążenia na port w puli adresów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="68a99-126">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="68a99-127">Reguły NAT ruchu przychodzącego — reguły mapowania portu publicznego modułu równoważenia obciążenia na port określonej maszyny wirtualnej w puli adresów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="68a99-127">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="68a99-128">Sondy — sondy kondycji używane do sprawdzania dostępności wystąpień maszyn wirtualnych w puli adresów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="68a99-128">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="68a99-129">Aby uzyskać więcej informacji, zobacz artykuł [Azure Resource Manager support for Load Balancer](load-balancer-arm.md) (Obsługa usługi Azure Resource Manager dla modułu równoważenia obciążenia).</span><span class="sxs-lookup"><span data-stu-id="68a99-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-to-use-resource-manager"></a><span data-ttu-id="68a99-130">Konfigurowanie programu PowerShell do korzystania z usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="68a99-130">Set up PowerShell to use Resource Manager</span></span>

<span data-ttu-id="68a99-131">Upewnij się, że masz najnowszej wersji produkcyjnej moduł usługi Azure Resource Manager dla środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68a99-131">Make sure you have the latest production version of the Azure Resource Manager module for PowerShell.</span></span>

1. <span data-ttu-id="68a99-132">Zaloguj się do platformy Azure</span><span class="sxs-lookup"><span data-stu-id="68a99-132">Sign into Azure</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="68a99-133">Po wyświetleniu monitu wprowadź poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="68a99-133">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="68a99-134">Sprawdź subskrypcje dostępne na koncie.</span><span class="sxs-lookup"><span data-stu-id="68a99-134">Check the subscriptions for the account</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="68a99-135">Wybierz subskrypcję platformy Azure do użycia.</span><span class="sxs-lookup"><span data-stu-id="68a99-135">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="68a99-136">Utwórz grupę zasobów (Pomiń ten krok, jeśli przy użyciu istniejącej grupy zasobów)</span><span class="sxs-lookup"><span data-stu-id="68a99-136">Create a resource group (skip this step if using an existing resource group)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-the-front-end-ip-pool"></a><span data-ttu-id="68a99-137">Tworzenie sieci wirtualnej oraz publicznego adresu IP dla puli adresów IP frontonu</span><span class="sxs-lookup"><span data-stu-id="68a99-137">Create a virtual network and a public IP address for the front-end IP pool</span></span>

1. <span data-ttu-id="68a99-138">Utwórz sieć wirtualną z podsiecią.</span><span class="sxs-lookup"><span data-stu-id="68a99-138">Create a virtual network with a subnet.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    $vnet = New-AzureRmvirtualNetwork -Name VNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="68a99-139">Utwórz zasoby (PIP) dla puli adresów IP frontonu Azure publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="68a99-139">Create Azure Public IP address (PIP) resources for the front-end IP address pool.</span></span>

    ```powershell
    $publicIPv4 = New-AzureRmPublicIpAddress -Name 'pub-ipv4' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -IpAddressVersion IPv4 -DomainNameLabel lbnrpipv4
    $publicIPv6 = New-AzureRmPublicIpAddress -Name 'pub-ipv6' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Dynamic -IpAddressVersion IPv6 -DomainNameLabel lbnrpipv6
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="68a99-140">Moduł równoważenia obciążenia używa etykieta domeny publicznego adresu IP jako prefiksu nazwy FQDN.</span><span class="sxs-lookup"><span data-stu-id="68a99-140">The load balancer uses the domain label of the public IP as prefix for its FQDN.</span></span> <span data-ttu-id="68a99-141">W tym przykładzie są nazwy FQDN *lbnrpipv4.westus.cloudapp.azure.com* i *lbnrpipv6.westus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="68a99-141">In this example, the FQDNs are *lbnrpipv4.westus.cloudapp.azure.com* and *lbnrpipv6.westus.cloudapp.azure.com*.</span></span>

## <a name="create-a-front-end-ip-configurations-and-a-back-end-address-pool"></a><span data-ttu-id="68a99-142">Tworzenie konfiguracji IP frontonu i puli adresów zaplecza</span><span class="sxs-lookup"><span data-stu-id="68a99-142">Create a Front-End IP configurations and a Back-End Address Pool</span></span>

1. <span data-ttu-id="68a99-143">Utwórz konfigurację adres frontonu, używający adresów publicznego adresu IP, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="68a99-143">Create front-end address configuration that uses the Public IP addresses you created.</span></span>

    ```powershell
    $FEIPConfigv4 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv4" -PublicIpAddress $publicIPv4
    $FEIPConfigv6 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv6" -PublicIpAddress $publicIPv6
    ```

2. <span data-ttu-id="68a99-144">Tworzenie puli adresów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="68a99-144">Create back-end address pools.</span></span>

    ```powershell
    $backendpoolipv4 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv4"
    $backendpoolipv6 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv6"
    ```

## <a name="create-lb-rules-nat-rules-a-probe-and-a-load-balancer"></a><span data-ttu-id="68a99-145">Tworzenie LB reguł, NAT reguły, badanie i równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="68a99-145">Create LB rules, NAT rules, a probe, and a load balancer</span></span>

<span data-ttu-id="68a99-146">W tym przykładzie opisano tworzenie następujących elementów:</span><span class="sxs-lookup"><span data-stu-id="68a99-146">This example creates the following items:</span></span>

* <span data-ttu-id="68a99-147">regułę NAT do tłumaczenia cały ruch przychodzący na porcie 443 do portu 4443</span><span class="sxs-lookup"><span data-stu-id="68a99-147">a NAT rule to translate all incoming traffic on port 443 to port 4443</span></span>
* <span data-ttu-id="68a99-148">Reguła modułu równoważenia obciążenia do równoważenia całego ruchu przychodzącego do portu 80 na port 80 adresów w puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="68a99-148">a load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span></span>
* <span data-ttu-id="68a99-149">reguły modułu równoważenia obciążenia umożliwiają połączenie RDP z maszyn wirtualnych do portu 3389.</span><span class="sxs-lookup"><span data-stu-id="68a99-149">a load balancer rule to allow RDP connection to the VMs on port 3389.</span></span>
* <span data-ttu-id="68a99-150">zasada sondowania, aby sprawdzić stan kondycji na stronie o nazwie *HealthProbe.aspx* lub usługi na porcie 8080</span><span class="sxs-lookup"><span data-stu-id="68a99-150">a probe rule to check the health status on a page named *HealthProbe.aspx* or a service on port 8080</span></span>
* <span data-ttu-id="68a99-151">Moduł równoważenia obciążenia, która używa tych obiektów</span><span class="sxs-lookup"><span data-stu-id="68a99-151">a load balancer that uses all these objects</span></span>

1. <span data-ttu-id="68a99-152">Utwórz reguły NAT.</span><span class="sxs-lookup"><span data-stu-id="68a99-152">Create the NAT rules.</span></span>

    ```powershell
    $inboundNATRule1v4 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev4" -FrontendIpConfiguration $FEIPConfigv4 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    $inboundNATRule1v6 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev6" -FrontendIpConfiguration $FEIPConfigv6 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    ```

2. <span data-ttu-id="68a99-153">Utwórz sondę kondycji.</span><span class="sxs-lookup"><span data-stu-id="68a99-153">Create a health probe.</span></span> <span data-ttu-id="68a99-154">Istnieją dwie metody konfiguracji sondy:</span><span class="sxs-lookup"><span data-stu-id="68a99-154">There are two ways to configure a probe:</span></span>

    <span data-ttu-id="68a99-155">Sonda HTTP</span><span class="sxs-lookup"><span data-stu-id="68a99-155">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="68a99-156">lub sondowaniem TCP</span><span class="sxs-lookup"><span data-stu-id="68a99-156">or TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -Protocol Tcp -Port 8080 -IntervalInSeconds 15 -ProbeCount 2
    $RDPprobe = New-AzureRmLoadBalancerProbeConfig -Name 'RDPprobe' -Protocol Tcp -Port 3389 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="68a99-157">Na przykład firma Microsoft będzie używany sond protokołu TCP.</span><span class="sxs-lookup"><span data-stu-id="68a99-157">For this example, we are going to use the TCP probes.</span></span>

3. <span data-ttu-id="68a99-158">Utwórz regułę modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="68a99-158">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule1v4 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv4" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $lbrule1v6 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv6" -FrontendIpConfiguration $FEIPConfigv6 -BackendAddressPool $backendpoolipv6 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $RDPrule = New-AzureRmLoadBalancerRuleConfig -Name "RDPrule" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $RDPprobe -Protocol Tcp -FrontendPort 3389 -BackendPort 3389
    ```

4. <span data-ttu-id="68a99-159">Utwórz moduł równoważenia obciążenia przy użyciu utworzonego wcześniej obiektów.</span><span class="sxs-lookup"><span data-stu-id="68a99-159">Create the load balancer using the previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name 'myNrpIPv6LB' -Location 'West US' -FrontendIpConfiguration $FEIPConfigv4,$FEIPConfigv6 -InboundNatRule $inboundNATRule1v6,$inboundNATRule1v4 -BackendAddressPool $backendpoolipv4,$backendpoolipv6 -Probe $healthProbe,$RDPprobe -LoadBalancingRule $lbrule1v4,$lbrule1v6,$RDPrule
    ```

## <a name="create-nics-for-the-back-end-vms"></a><span data-ttu-id="68a99-160">Tworzenie kart sieciowych w maszynach wirtualnych zaplecza</span><span class="sxs-lookup"><span data-stu-id="68a99-160">Create NICs for the back-end VMs</span></span>

1. <span data-ttu-id="68a99-161">Pobierz sieci wirtualnej i podsieci sieci wirtualnej, gdy karty te muszą zostać utworzone.</span><span class="sxs-lookup"><span data-stu-id="68a99-161">Get the Virtual Network and Virtual Network Subnet, where the NICs need to be created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name VNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="68a99-162">Tworzenie konfiguracji adresów IP i karty sieciowe dla maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="68a99-162">Create IP configurations and NICs for the VMs.</span></span>

    ```powershell
    $nic1IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4 -LoadBalancerInboundNatRule $inboundNATRule1v4
    $nic1IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6 -LoadBalancerInboundNatRule $inboundNATRule1v6
    $nic1 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic0' -IpConfiguration $nic1IPv4,$nic1IPv6 -ResourceGroupName NRP-RG -Location 'West US'

    $nic2IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4
    $nic2IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6
    $nic2 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic1' -IpConfiguration $nic2IPv4,$nic2IPv6 -ResourceGroupName NRP-RG -Location 'West US'
    ```

## <a name="create-virtual-machines-and-assign-the-newly-created-nics"></a><span data-ttu-id="68a99-163">Tworzenie maszyn wirtualnych i przypisz nowo utworzony kart sieciowych</span><span class="sxs-lookup"><span data-stu-id="68a99-163">Create virtual machines and assign the newly created NICs</span></span>

<span data-ttu-id="68a99-164">Aby uzyskać więcej informacji na temat tworzenia maszyny Wirtualnej, zobacz [Utwórz wstępnie skonfigurowaną maszynę wirtualną systemu Windows z usługi Resource Manager i programu Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="68a99-164">For more information about creating a VM, see [Create and preconfigure a Windows Virtual Machine with Resource Manager and Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="68a99-165">Tworzenie zestawu dostępności i konto magazynu</span><span class="sxs-lookup"><span data-stu-id="68a99-165">Create an Availability Set and Storage account</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG -location 'West US'
    $availabilitySet = Get-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG
    New-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct' -Location 'West US' -SkuName "Standard_LRS"
    $CreatedStorageAccount = Get-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct'
    ```

2. <span data-ttu-id="68a99-166">Utwórz każdej maszyny Wirtualnej i przypisz poprzedniej karty sieciowe utworzone</span><span class="sxs-lookup"><span data-stu-id="68a99-166">Create each VM and assign the previous created NICs</span></span>

    ```powershell
    $mySecureCredentials= Get-Credential -Message "Type the username and password of the local administrator account."

    $vm1 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM0' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm1 = Set-AzureRmVMOperatingSystem -VM $vm1 -Windows -ComputerName 'myNrpIPv6VM0' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm1 = Set-AzureRmVMSourceImage -VM $vm1 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm1 = Add-AzureRmVMNetworkInterface -VM $vm1 -Id $nic1.Id -Primary
    $osDisk1Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM0osdisk.vhd"
    $vm1 = Set-AzureRmVMOSDisk -VM $vm1 -Name 'myNrpIPv6VM0osdisk' -VhdUri $osDisk1Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm1

    $vm2 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM1' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm2 = Set-AzureRmVMOperatingSystem -VM $vm2 -Windows -ComputerName 'myNrpIPv6VM1' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm2 = Set-AzureRmVMSourceImage -VM $vm2 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm2 = Add-AzureRmVMNetworkInterface -VM $vm2 -Id $nic2.Id -Primary
    $osDisk2Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM1osdisk.vhd"
    $vm2 = Set-AzureRmVMOSDisk -VM $vm2 -Name 'myNrpIPv6VM1osdisk' -VhdUri $osDisk2Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm2
    ```

## <a name="next-steps"></a><span data-ttu-id="68a99-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="68a99-167">Next steps</span></span>

<span data-ttu-id="68a99-168">[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-ps.md) (Wprowadzenie do konfigurowania wewnętrznego modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="68a99-168">[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-ps.md)</span></span>

<span data-ttu-id="68a99-169">[Configure a load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="68a99-169">[Configure a load balancer distribution mode](load-balancer-distribution-mode.md)</span></span>

<span data-ttu-id="68a99-170">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="68a99-170">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md)</span></span>
