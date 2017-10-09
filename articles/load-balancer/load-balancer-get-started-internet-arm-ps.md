---
title: "Moduł równoważenia - obciążenia aaaCreate Azure internetowy, programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate internetowy modułu równoważenia obciążenia w Menedżerze zasobów przy użyciu programu PowerShell"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 8257f548-7019-417f-b15f-d004a1eec826
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e4e0e5271bc83c23fc62c0910e784c57d2b30065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="7af56-103"><a name="get-started"></a>Tworzenie dostępnego z Internetu modułu równoważenia obciążenia w usłudze Resource Manager za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="7af56-103"><a name="get-started"></a>Creating an Internet-facing load balancer in Resource Manager by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7af56-104">Portal</span><span class="sxs-lookup"><span data-stu-id="7af56-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="7af56-105">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="7af56-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="7af56-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7af56-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="7af56-107">Szablon</span><span class="sxs-lookup"><span data-stu-id="7af56-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="7af56-108">W tym artykule omówiono modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="7af56-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="7af56-109">Możesz również [Dowiedz się, jak toocreate internetowy modułu równoważenia obciążenia przy użyciu hello klasycznego modelu wdrażania](load-balancer-get-started-internet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7af56-109">You can also [learn how toocreate an Internet-facing load balancer by using hello classic deployment model](load-balancer-get-started-internet-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-by-using-azure-powershell"></a><span data-ttu-id="7af56-110">Wdrażanie rozwiązania hello przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7af56-110">Deploying hello solution by using Azure PowerShell</span></span>

<span data-ttu-id="7af56-111">Witaj, zgodnie z procedurami wyjaśniają, jak toocreate internetowy modułu równoważenia obciążenia przy użyciu usługi Azure Resource Manager przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7af56-111">hello following procedures explain how toocreate an Internet-facing load balancer by using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="7af56-112">Usługi Azure Resource Manager każdy zasób jest tworzony i skonfigurować osobno, a następnie umieść razem toocreate modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="7af56-112">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a load balancer.</span></span>

<span data-ttu-id="7af56-113">Należy utworzyć i skonfigurować hello następujące obiekty toodeploy modułu równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="7af56-113">You must create and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="7af56-114">Konfiguracja IP frontonu — publiczne adresy IP (PIP) dla przychodzącego ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="7af56-114">Front-end IP configuration: contains public IP (PIP) addresses for incoming network traffic.</span></span>
* <span data-ttu-id="7af56-115">Pula adresów zaplecza: zawiera interfejsów sieciowych (NIC) dla ruchu sieciowego tooreceive hello maszyn wirtualnych z hello modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="7af56-115">Back-end address pool: contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="7af56-116">Reguły równoważenia obciążenia: zawiera reguły, które mapują port publiczny na porcie programu tooa usługi równoważenia obciążenia w hello w puli adresów zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="7af56-116">Load-balancing rules: contains rules that map a public port on hello load balancer tooa port in hello back-end address pool.</span></span>
* <span data-ttu-id="7af56-117">Reguły NAT dla ruchu przychodzącego: zawiera reguły, które mapują port publiczny na porcie programu tooa usługi równoważenia obciążenia w hello dla określonej maszyny wirtualnej w puli adresów zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="7af56-117">Inbound NAT rules: contains rules that map a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="7af56-118">Sondy: zawiera dostępność toocheck badania używane kondycji wystąpień maszyn wirtualnych w puli adresów zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="7af56-118">Probes: contains health probes used toocheck availability of virtual machine instances in hello back-end address pool.</span></span>

<span data-ttu-id="7af56-119">Aby uzyskać więcej informacji, zobacz artykuł [Azure Resource Manager support for Load Balancer](load-balancer-arm.md) (Obsługa usługi Azure Resource Manager dla modułu równoważenia obciążenia).</span><span class="sxs-lookup"><span data-stu-id="7af56-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-toouse-resource-manager"></a><span data-ttu-id="7af56-120">Konfigurowanie środowiska PowerShell toouse Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7af56-120">Set up PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="7af56-121">Upewnij się, że masz hello najnowszej wersji produkcyjnej hello moduł usługi Azure Resource Manager dla środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7af56-121">Make sure you have hello latest production version of hello Azure Resource Manager module for PowerShell:</span></span>

1. <span data-ttu-id="7af56-122">Zaloguj się tooAzure.</span><span class="sxs-lookup"><span data-stu-id="7af56-122">Sign in tooAzure.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="7af56-123">Po wyświetleniu monitu wprowadź poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="7af56-123">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="7af56-124">Sprawdź subskrypcje hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="7af56-124">Check hello subscriptions for hello account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="7af56-125">Wybierz z toouse Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7af56-125">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="7af56-126">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="7af56-126">Create a resource group.</span></span> <span data-ttu-id="7af56-127">(Pomiń ten krok, jeśli używasz istniejącej grupy zasobów).</span><span class="sxs-lookup"><span data-stu-id="7af56-127">(Skip this step if you're using an existing resource group.)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="7af56-128">Tworzenie sieci wirtualnej i publiczny adres IP dla puli adresów IP frontonu hello</span><span class="sxs-lookup"><span data-stu-id="7af56-128">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="7af56-129">Utwórz podsieć i sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="7af56-129">Create a subnet and a virtual network.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="7af56-130">Utwórz Azure publicznego zasób adresu IP, o nazwie **publicznego adresu IP**, toobe używane przez pulę IP frontonu z nazwą DNS hello **loadbalancernrp.westus.cloudapp.azure.com**. hello następujące polecenia używa hello Typ alokacji statycznych.</span><span class="sxs-lookup"><span data-stu-id="7af56-130">Create an Azure public IP address resource, named **PublicIP**, toobe used by a front-end IP pool with hello DNS name **loadbalancernrp.westus.cloudapp.azure.com**. hello following command uses hello static allocation type.</span></span>

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="7af56-131">Moduł równoważenia obciążenia Hello używa hello etykieta domeny publicznego adresu IP hello jako prefiksu dla nazwy FQDN.</span><span class="sxs-lookup"><span data-stu-id="7af56-131">hello load balancer uses hello domain label of hello public IP as a prefix for its FQDN.</span></span> <span data-ttu-id="7af56-132">To jest inna niż hello wdrażania klasycznego modelu, który używa usługi w chmurze hello hello równoważenia obciążenia w pełni kwalifikowaną nazwę domeny.</span><span class="sxs-lookup"><span data-stu-id="7af56-132">This is different from hello classic deployment model, which uses hello cloud service as hello load balancer FQDN.</span></span>
   > <span data-ttu-id="7af56-133">W tym przykładzie hello nazwy FQDN jest **loadbalancernrp.westus.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="7af56-133">In this example, hello FQDN is **loadbalancernrp.westus.cloudapp.azure.com**.</span></span>

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a><span data-ttu-id="7af56-134">Tworzenie puli adresów IP frontonu i puli adresów zaplecza</span><span class="sxs-lookup"><span data-stu-id="7af56-134">Create a front-end IP pool and a back-end address pool</span></span>

1. <span data-ttu-id="7af56-135">Utwórz pulę IP frontonu o nazwie **LB frontonu** używającą hello **PublicIp** zasobów.</span><span class="sxs-lookup"><span data-stu-id="7af56-135">Create a front-end IP pool named **LB-Frontend** that uses hello **PublicIp** resource.</span></span>

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. <span data-ttu-id="7af56-136">Utwórz pulę adresów zaplecza o nazwie **LB-backend**.</span><span class="sxs-lookup"><span data-stu-id="7af56-136">Create a back-end address pool named **LB-backend**.</span></span>

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a><span data-ttu-id="7af56-137">Tworzenie reguł NAT, reguł modułu równoważenia obciążenia, sondy oraz modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="7af56-137">Create NAT rules, a load balancer rule, a probe, and a load balancer</span></span>

<span data-ttu-id="7af56-138">W tym przykładzie jest tworzony hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="7af56-138">This example creates hello following items:</span></span>

* <span data-ttu-id="7af56-139">Wszystkie przychodzący ruch na porcie 3441 tooport 3389 tootranslate reguły NAT</span><span class="sxs-lookup"><span data-stu-id="7af56-139">A NAT rule tootranslate all incoming traffic on port 3441 tooport 3389</span></span>
* <span data-ttu-id="7af56-140">Wszystkie przychodzący ruch na porcie 3442 tooport 3389 tootranslate reguły NAT</span><span class="sxs-lookup"><span data-stu-id="7af56-140">A NAT rule tootranslate all incoming traffic on port 3442 tooport 3389</span></span>
* <span data-ttu-id="7af56-141">Stan kondycji sondowania reguł toocheck hello na stronie o nazwie **HealthProbe.aspx**</span><span class="sxs-lookup"><span data-stu-id="7af56-141">A probe rule toocheck hello health status on a page named **HealthProbe.aspx**</span></span>
* <span data-ttu-id="7af56-142">Toobalance reguły modułu równoważenia obciążenia cały ruch przychodzący na porcie 80 tooport 80 na powitania adresy w puli zaplecza hello</span><span class="sxs-lookup"><span data-stu-id="7af56-142">A load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool</span></span>
* <span data-ttu-id="7af56-143">Modułu równoważenia obciążenia, który korzysta ze wszystkich wymienionych obiektów</span><span class="sxs-lookup"><span data-stu-id="7af56-143">A load balancer that uses all these objects</span></span>

<span data-ttu-id="7af56-144">Wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7af56-144">Use these steps:</span></span>

1. <span data-ttu-id="7af56-145">Tworzenie reguł NAT hello.</span><span class="sxs-lookup"><span data-stu-id="7af56-145">Create hello NAT rules.</span></span>

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. <span data-ttu-id="7af56-146">Utwórz sondę kondycji.</span><span class="sxs-lookup"><span data-stu-id="7af56-146">Create a health probe.</span></span> <span data-ttu-id="7af56-147">Istnieją dwa sposoby tooconfigure badanie:</span><span class="sxs-lookup"><span data-stu-id="7af56-147">There are two ways tooconfigure a probe:</span></span>

    <span data-ttu-id="7af56-148">Sonda HTTP</span><span class="sxs-lookup"><span data-stu-id="7af56-148">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="7af56-149">Sonda TCP</span><span class="sxs-lookup"><span data-stu-id="7af56-149">TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. <span data-ttu-id="7af56-150">Utwórz regułę modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="7af56-150">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. <span data-ttu-id="7af56-151">Utwórz hello modułu równoważenia obciążenia za pomocą obiektów hello wcześniej utworzony.</span><span class="sxs-lookup"><span data-stu-id="7af56-151">Create hello load balancer by using hello previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a><span data-ttu-id="7af56-152">Tworzenie kart sieciowych</span><span class="sxs-lookup"><span data-stu-id="7af56-152">Create NICs</span></span>

<span data-ttu-id="7af56-153">Tworzenie interfejsów sieciowych (lub modyfikować istniejące) i kojarzyć je tooNAT reguły, reguły modułu równoważenia obciążenia i sond:</span><span class="sxs-lookup"><span data-stu-id="7af56-153">Create network interfaces (or modify existing ones) and then associate them tooNAT rules, load balancer rules, and probes:</span></span>

1. <span data-ttu-id="7af56-154">Pobierz hello sieć wirtualna i podsieć sieci wirtualnej, której hello karty sieciowe muszą toobe utworzony.</span><span class="sxs-lookup"><span data-stu-id="7af56-154">Get hello virtual network and a virtual network subnet, where hello NICs need toobe created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="7af56-155">Utwórz kartę Sieciową o nazwie **można nic1 lb**i skojarz go z pierwszej reguły NAT hello i puli adresów zaplecza pierwszy (i tylko) hello.</span><span class="sxs-lookup"><span data-stu-id="7af56-155">Create a NIC named **lb-nic1-be**, and associate it with hello first NAT rule and hello first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. <span data-ttu-id="7af56-156">Utwórz kartę Sieciową o nazwie **można nic2 lb**i skojarz go z drugą regułę NAT hello i puli adresów zaplecza pierwszy (i tylko) hello.</span><span class="sxs-lookup"><span data-stu-id="7af56-156">Create a NIC named **lb-nic2-be**, and associate it with hello second NAT rule and hello first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. <span data-ttu-id="7af56-157">Sprawdź hello kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="7af56-157">Check hello NICs.</span></span>

        $backendnic1

    <span data-ttu-id="7af56-158">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="7af56-158">Expected output:</span></span>

        Name                 : lb-nic1-be
        ResourceGroupName    : NRP-RG
        Location             : westus
        Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
        ResourceGuid         : 896cac4f-152a-40b9-b079-3e2201a5906e
        ProvisioningState    : Succeeded
        Tags                 :
        VirtualMachine       : null
        IpConfigurations     : [
                            {
                            "Name": "ipconfig1",
                            "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                            "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1",
                            "PrivateIpAddress": "10.0.2.6",
                            "PrivateIpAllocationMethod": "Static",
                            "Subnet": {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                            },
                            "ProvisioningState": "Succeeded",
                            "PrivateIpAddressVersion": "IPv4",
                            "PublicIpAddress": {
                                "Id": null
                            },
                            "LoadBalancerBackendAddressPools": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/backendAddressPools/LB-backend"
                                }
                            ],
                            "LoadBalancerInboundNatRules": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/inboundNatRules/RDP1"
                                }
                            ],
                            "Primary": true,
                            "ApplicationGatewayBackendAddressPools": []
                            }
                        ]
        DnsSettings          : {
                            "DnsServers": [],
                            "AppliedDnsServers": [],
                            "InternalDomainNameSuffix": "prcwibzcuvie5hnxav0yjks2cd.dx.internal.cloudapp.net"
                        }
        EnableIPForwarding   : False
        NetworkSecurityGroup : null
        Primary              :

5. <span data-ttu-id="7af56-159">Użyj hello `Add-AzureRmVMNetworkInterface` polecenia cmdlet tooassign hello kart sieciowych toodifferent maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="7af56-159">Use hello `Add-AzureRmVMNetworkInterface` cmdlet tooassign hello NICs toodifferent VMs.</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="7af56-160">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7af56-160">Create a virtual machine</span></span>

<span data-ttu-id="7af56-161">Wskazówki dotyczące tworzenia maszyny wirtualnej i przypisywania karty sieciowej znajdują się w artykule [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) (Tworzenie maszyny wirtualnej Azure za pomocą programu PowerShell).</span><span class="sxs-lookup"><span data-stu-id="7af56-161">For guidance on creating a virtual machine and assigning a NIC, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-hello-network-interface-toohello-load-balancer"></a><span data-ttu-id="7af56-162">Dodaj usługi równoważenia obciążenia toohello hello sieciowych — Interfejs</span><span class="sxs-lookup"><span data-stu-id="7af56-162">Add hello network interface toohello load balancer</span></span>

1. <span data-ttu-id="7af56-163">Pobrać hello modułu równoważenia obciążenia z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7af56-163">Retrieve hello load balancer from Azure.</span></span>

    <span data-ttu-id="7af56-164">Ładowanie zasobów usługi równoważenia obciążenia hello do zmiennej (Jeśli użytkownik jeszcze nie).</span><span class="sxs-lookup"><span data-stu-id="7af56-164">Load hello load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="7af56-165">Zmienna Hello jest nazywany **$lb**. Użyj hello takie same nazwy z hello zasobów usługi równoważenia obciążenia, utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="7af56-165">hello variable is called **$lb**. Use hello same names from hello load balancer resource that you created earlier.</span></span>

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. <span data-ttu-id="7af56-166">Zmienna tooa konfiguracji zaplecza hello obciążenia.</span><span class="sxs-lookup"><span data-stu-id="7af56-166">Load hello back-end configuration tooa variable.</span></span>

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. <span data-ttu-id="7af56-167">Załaduj hello już utworzone, interfejs sieciowy do zmiennej.</span><span class="sxs-lookup"><span data-stu-id="7af56-167">Load hello already created network interface into a variable.</span></span> <span data-ttu-id="7af56-168">Nazwa zmiennej Hello jest **$nic**.</span><span class="sxs-lookup"><span data-stu-id="7af56-168">hello variable name is **$nic**.</span></span> <span data-ttu-id="7af56-169">Witaj Nazwa interfejsu sieciowego jest hello jednego z hello wcześniejszego przykładu.</span><span class="sxs-lookup"><span data-stu-id="7af56-169">hello network interface name is hello same one from hello earlier example.</span></span>

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. <span data-ttu-id="7af56-170">Zmień konfigurację zaplecza hello na powitania interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="7af56-170">Change hello back-end configuration on hello network interface.</span></span>

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. <span data-ttu-id="7af56-171">Zapisz obiekt interfejsu sieciowego hello.</span><span class="sxs-lookup"><span data-stu-id="7af56-171">Save hello network interface object.</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    <span data-ttu-id="7af56-172">Po dodaniu interfejsu sieciowego puli zaplecza modułu równoważenia obciążenia toohello uruchamia odbieranie ruchu sieciowego na podstawie hello reguł równoważenia obciążenia dla tego zasobu usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="7af56-172">After a network interface is added toohello load balancer back-end pool, it starts receiving network traffic based on hello load-balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="7af56-173">Aktualizowanie istniejącego modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="7af56-173">Update an existing load balancer</span></span>

1. <span data-ttu-id="7af56-174">Za pomocą hello załadować równoważenia z wcześniejszego przykładu hello, należy przypisać zmiennej toohello obiekt usługi równoważenia obciążenia **$slb** przy użyciu `Get-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="7af56-174">By using hello load balancer from hello earlier example, assign a load balancer object toohello variable **$slb** by using `Get-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. <span data-ttu-id="7af56-175">W hello poniższy przykład możesz dodać regułę ruchu przychodzącego translatora adresów Sieciowych — przy użyciu portu 81 hello puli frontonu i 8181 puli zaplecza hello--tooan istniejący moduł równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="7af56-175">In hello following example, you add an inbound NAT rule--by using port 81 in hello front-end pool and port 8181 for hello back-end pool--tooan existing load balancer.</span></span>

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. <span data-ttu-id="7af56-176">Zapisz nową konfigurację hello przy użyciu `Set-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="7af56-176">Save hello new configuration by using `Set-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="7af56-177">Usuwanie modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="7af56-177">Remove a load balancer</span></span>

<span data-ttu-id="7af56-178">Użyj polecenia hello `Remove-AzureLoadBalancer` toodelete modułu równoważenia obciążenia utworzonej wcześniej o nazwie **NRP LB** w grupie zasobów o nazwie **zarządcy zasobów NRP**.</span><span class="sxs-lookup"><span data-stu-id="7af56-178">Use hello command `Remove-AzureLoadBalancer` toodelete a previously created load balancer named **NRP-LB** in a resource group called **NRP-RG**.</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="7af56-179">Można użyć przełącznika opcjonalne hello **-Force** tooavoid hello wiersza do usunięcia.</span><span class="sxs-lookup"><span data-stu-id="7af56-179">You can use hello optional switch **-Force** tooavoid hello prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7af56-180">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7af56-180">Next steps</span></span>

<span data-ttu-id="7af56-181">[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-ps.md) (Wprowadzenie do konfigurowania wewnętrznego modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="7af56-181">[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-ps.md)</span></span>

<span data-ttu-id="7af56-182">[Configure a load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="7af56-182">[Configure a load balancer distribution mode](load-balancer-distribution-mode.md)</span></span>

<span data-ttu-id="7af56-183">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="7af56-183">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md)</span></span>
