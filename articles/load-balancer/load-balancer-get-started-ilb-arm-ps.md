---
title: "Moduł równoważenia - obciążenia aaaCreate wewnętrznego Azure, programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usługa równoważenia przy użyciu programu PowerShell w Menedżerze zasobów obciążenia toocreate jako wewnętrzne"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c6c98981-df9d-4dd7-a94b-cc7d1dc99369
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 4b9657c77aa32a142de49ff7871ed6a396b22223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a><span data-ttu-id="6cf43-103">Tworzenie wewnętrznego modułu równoważenia obciążenia przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="6cf43-103">Create an internal load balancer using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6cf43-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6cf43-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="6cf43-105">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="6cf43-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="6cf43-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6cf43-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="6cf43-107">Szablon</span><span class="sxs-lookup"><span data-stu-id="6cf43-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="6cf43-108">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6cf43-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="6cf43-109">W tym artykule omówiono przy użyciu modelu wdrażania Menedżera zasobów hello, który firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello [klasycznego modelu wdrażania](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="6cf43-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

<span data-ttu-id="6cf43-110">Witaj, wykonaj czynności wyjaśniają, jak toocreate jako wewnętrzne obciążenia przy użyciu usługi Azure Resource Manager przy użyciu programu PowerShell usługi równoważenia.</span><span class="sxs-lookup"><span data-stu-id="6cf43-110">hello following steps explain how toocreate an internal load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="6cf43-111">Usługi Azure Resource Manager hello elementów toocreate wewnętrznego modułu równoważenia obciążenia są konfigurowane osobno, a następnie łączyć toocreate modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="6cf43-111">With Azure Resource Manager, hello items toocreate a Internal load balancer are configured individually and then combined toocreate a load balancer.</span></span>

<span data-ttu-id="6cf43-112">Należy toocreate i skonfigurować hello następujące obiekty toodeploy modułu równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="6cf43-112">You need toocreate and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="6cf43-113">FrontPage zakończenia konfiguracji IP — skonfiguruje hello prywatnego adresu IP dla przychodzącego ruchu sieciowego</span><span class="sxs-lookup"><span data-stu-id="6cf43-113">Front end IP configuration - will configure hello private IP address for incoming network traffic</span></span>
* <span data-ttu-id="6cf43-114">Pula adresów zaplecza - skonfiguruje hello interfejsów sieciowych, które otrzymają ruchu o zrównoważonym obciążeniu hello pochodzące z puli adresów IP frontonu</span><span class="sxs-lookup"><span data-stu-id="6cf43-114">Backend address pool - will configure hello network interfaces which will receive hello load balanced traffic coming from front end IP pool</span></span>
* <span data-ttu-id="6cf43-115">Reguły równoważenia obciążenia — źródło i Konfiguracja portów lokalnych dla hello modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="6cf43-115">Load balancing rules - source and local port configuration for hello load balancer.</span></span>
* <span data-ttu-id="6cf43-116">Sondy — konfiguruje sondowania stanu kondycji hello hello wystąpień maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6cf43-116">Probes - configures hello health status probe for hello Virtual Machine instances.</span></span>
* <span data-ttu-id="6cf43-117">Reguły NAT dla ruchu przychodzącego — służy do konfigurowania dostępu toodirectly reguły portu hello, jeden hello wystąpień maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="6cf43-117">Inbound NAT rules - configures hello port rules toodirectly access one of hello Virtual Machine instances.</span></span>

<span data-ttu-id="6cf43-118">Więcej informacji o składnikach modułu równoważenia obciążenia tworzonego za pomocą usługi Azure Resource Manager można znaleźć w artykule [Azure Resource Manager support for load balancer](load-balancer-arm.md) (Obsługa usługi Azure Resource Manager dla modułu równoważenia obciążenia).</span><span class="sxs-lookup"><span data-stu-id="6cf43-118">You can get more information about load balancer components with Azure resource manager at [Azure Resource Manager support for load balancer](load-balancer-arm.md).</span></span>

<span data-ttu-id="6cf43-119">Witaj poniższych krokach opisano sposób tooconfigure modułu równoważenia obciążenia między dwiema maszynami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="6cf43-119">hello following steps explain how tooconfigure a load balancer between two virtual machines.</span></span>

## <a name="setup-powershell-toouse-resource-manager"></a><span data-ttu-id="6cf43-120">Instalator programu PowerShell toouse Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6cf43-120">Setup PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="6cf43-121">Upewnij się, możesz mają hello najnowszej wersji produkcyjnej hello Azure modułu środowiska PowerShell i programu PowerShell Instalatora poprawnie tooaccess subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6cf43-121">Make sure you have hello latest production version of hello Azure module for PowerShell, and have PowerShell setup correctly tooaccess your Azure subscription.</span></span>

### <a name="step-1"></a><span data-ttu-id="6cf43-122">Krok 1</span><span class="sxs-lookup"><span data-stu-id="6cf43-122">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="6cf43-123">Krok 2</span><span class="sxs-lookup"><span data-stu-id="6cf43-123">Step 2</span></span>

<span data-ttu-id="6cf43-124">Sprawdź subskrypcje hello hello konta</span><span class="sxs-lookup"><span data-stu-id="6cf43-124">Check hello subscriptions for hello account</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="6cf43-125">Zostanie wyświetlony monit o tooAuthenticate będzie przy użyciu poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="6cf43-125">You will be prompted tooAuthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="6cf43-126">Krok 3</span><span class="sxs-lookup"><span data-stu-id="6cf43-126">Step 3</span></span>

<span data-ttu-id="6cf43-127">Wybierz z toouse Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6cf43-127">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a><span data-ttu-id="6cf43-128">Tworzenie grupy zasobów dla modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="6cf43-128">Create Resource Group for load balancer</span></span>

<span data-ttu-id="6cf43-129">Utwórz nową grupę zasobów (ten krok można pominąć, jeśli używasz istniejącej grupy zasobów).</span><span class="sxs-lookup"><span data-stu-id="6cf43-129">Create a new resource group (skip this step if using an existing resource group)</span></span>

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

<span data-ttu-id="6cf43-130">Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację.</span><span class="sxs-lookup"><span data-stu-id="6cf43-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="6cf43-131">Służy to jako hello domyślna lokalizacja dla zasobów w danej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="6cf43-131">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="6cf43-132">Upewnić się, że wszystkie polecenia toocreate modułu równoważenia obciążenia będzie używać hello same grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="6cf43-132">Make sure all commands toocreate a load balancer will use hello same resource group.</span></span>

<span data-ttu-id="6cf43-133">W hello przykład powyżej firma Microsoft utworzone grupy zasobów o nazwie "Zarządcy zasobów NRP" i lokalizacji "Zachodnie US".</span><span class="sxs-lookup"><span data-stu-id="6cf43-133">In hello example above we created a resource group called "NRP-RG" and location "West US".</span></span>

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a><span data-ttu-id="6cf43-134">Tworzenie sieci wirtualnej i prywatnego adresu IP dla puli adresów IP frontonu</span><span class="sxs-lookup"><span data-stu-id="6cf43-134">Create Virtual Network and a private IP address for front end IP pool</span></span>

<span data-ttu-id="6cf43-135">Tworzy podsieć sieci wirtualnej hello i przypisuje toovariable $backendSubnet</span><span class="sxs-lookup"><span data-stu-id="6cf43-135">Creates a subnet for hello virtual network and assigns toovariable $backendSubnet</span></span>

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

<span data-ttu-id="6cf43-136">Utwórz sieć wirtualną:</span><span class="sxs-lookup"><span data-stu-id="6cf43-136">Create a virtual network:</span></span>

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

<span data-ttu-id="6cf43-137">Tworzy hello sieci wirtualnej i dodaje hello podsieci można podsieci lb toohello sieci wirtualnej NRPVNet i przypisuje toovariable $vnet</span><span class="sxs-lookup"><span data-stu-id="6cf43-137">Creates hello virtual network and adds hello subnet lb-subnet-be toohello virtual network NRPVNet and assigns toovariable $vnet</span></span>

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a><span data-ttu-id="6cf43-138">Tworzenie puli adresów IP frontonu i puli adresów zaplecza</span><span class="sxs-lookup"><span data-stu-id="6cf43-138">Create Front end IP pool and backend address pool</span></span>

<span data-ttu-id="6cf43-139">Konfigurowanie puli IP frontonu dla hello przychodzące obciążenia modułu równoważenia obciążenia sieci i wewnętrznej bazy danych adresów puli tooreceive hello ze zrównoważonym obciążeniem ruchu.</span><span class="sxs-lookup"><span data-stu-id="6cf43-139">Setting up a front end IP pool for hello incoming load balancer network traffic and backend address pool tooreceive hello load balanced traffic.</span></span>

### <a name="step-1"></a><span data-ttu-id="6cf43-140">Krok 1</span><span class="sxs-lookup"><span data-stu-id="6cf43-140">Step 1</span></span>

<span data-ttu-id="6cf43-141">Utwórz pulę IP frontonu przy użyciu prywatnego adresu IP hello 10.0.2.5 dla hello podsieci 10.0.2.0/24 którego będzie punktu końcowego hello przychodzącego sieci ruchu.</span><span class="sxs-lookup"><span data-stu-id="6cf43-141">Create a front end IP pool using hello private IP address 10.0.2.5 for hello subnet 10.0.2.0/24 which will be hello incoming network traffic endpoint.</span></span>

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a><span data-ttu-id="6cf43-142">Krok 2</span><span class="sxs-lookup"><span data-stu-id="6cf43-142">Step 2</span></span>

<span data-ttu-id="6cf43-143">Konfigurowanie puli adresów zaplecza używane tooreceive ruch przychodzący z puli adresów IP frontonu:</span><span class="sxs-lookup"><span data-stu-id="6cf43-143">Set up a back end address pool used tooreceive incoming traffic from front end IP pool:</span></span>

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a><span data-ttu-id="6cf43-144">Tworzenie reguł równoważenia obciążenia, reguł NAT, sondy i modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="6cf43-144">Create LB rules, NAT rules, probe and load balancer</span></span>

<span data-ttu-id="6cf43-145">Po utworzeniu puli adresów IP frontonu hello i puli adresów zaplecza hello, konieczne będzie toocreate hello reguł, które będą należeć zasób usługi równoważenia obciążenia toohello:</span><span class="sxs-lookup"><span data-stu-id="6cf43-145">After creating hello front end IP pool and hello backend address pool, you will need toocreate hello rules which will belong toohello load balancer resource:</span></span>

### <a name="step-1"></a><span data-ttu-id="6cf43-146">Krok 1</span><span class="sxs-lookup"><span data-stu-id="6cf43-146">Step 1</span></span>

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

<span data-ttu-id="6cf43-147">w powyższym przykładzie Hello jest tworzenie hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6cf43-147">hello example above is creating hello following items:</span></span>

* <span data-ttu-id="6cf43-148">Reguła NAT, w którym cały ruch przychodzący ruch tooport 3441 przejdzie tooport 3389.</span><span class="sxs-lookup"><span data-stu-id="6cf43-148">NAT rule which all incoming traffic tooport 3441 will go tooport 3389.</span></span>
* <span data-ttu-id="6cf43-149">drugą regułę NAT, w którym cały ruch przychodzący ruch tooport 3442 przejdzie tooport 3389.</span><span class="sxs-lookup"><span data-stu-id="6cf43-149">a second NAT rule which all incoming traffic tooport 3442 will go tooport 3389.</span></span>
* <span data-ttu-id="6cf43-150">reguły modułu równoważenia obciążenia, który zostanie załadowany równoważenie cały ruch przychodzący port publiczny 80 toolocal portu 80 w puli adresów zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="6cf43-150">a load balancer rule which will load balance all incoming traffic on public port 80 toolocal port 80 in hello back end address pool.</span></span>
* <span data-ttu-id="6cf43-151">zasada sondowania, który będzie sprawdzać stan kondycji powitania dla ścieżki "HealthProbe.aspx"</span><span class="sxs-lookup"><span data-stu-id="6cf43-151">a probe rule which will check hello health status for path "HealthProbe.aspx"</span></span>

### <a name="step-2"></a><span data-ttu-id="6cf43-152">Krok 2</span><span class="sxs-lookup"><span data-stu-id="6cf43-152">Step 2</span></span>

<span data-ttu-id="6cf43-153">Utwórz moduł równoważenia obciążenia hello zsumowanie wszystkie obiekty (reguł NAT, reguły modułu równoważenia obciążenia, konfiguracje sondowania):</span><span class="sxs-lookup"><span data-stu-id="6cf43-153">Create hello load balancer adding all objects (NAT rules, Load balancer rules, probe configurations) together:</span></span>

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a><span data-ttu-id="6cf43-154">Tworzenie interfejsów sieciowych</span><span class="sxs-lookup"><span data-stu-id="6cf43-154">Create network interfaces</span></span>

<span data-ttu-id="6cf43-155">Po utworzeniu hello wewnętrznego modułu równoważenia obciążenia, należy zdefiniować interfejsów sieciowych, który będzie otrzymywał hello przychodzącego ze zrównoważonym obciążeniem ruchu sieciowego, reguł NAT i badania.</span><span class="sxs-lookup"><span data-stu-id="6cf43-155">After creating hello internal load balancer, you need define which network interfaces will be receiving hello incoming load balanced network traffic, NAT rules and probe.</span></span> <span data-ttu-id="6cf43-156">w takim przypadku Hello interfejs sieciowy jest konfigurowane osobno i można przypisać tooa maszyny wirtualnej na dalszym etapie.</span><span class="sxs-lookup"><span data-stu-id="6cf43-156">hello network interface in this case is configured individually and can be assigned tooa virtual machine later on.</span></span>

### <a name="step-1"></a><span data-ttu-id="6cf43-157">Krok 1</span><span class="sxs-lookup"><span data-stu-id="6cf43-157">Step 1</span></span>

<span data-ttu-id="6cf43-158">Pobierz zasób hello wirtualnych sieci i podsieci interfejsy toocreate w sieci:</span><span class="sxs-lookup"><span data-stu-id="6cf43-158">Get hello resource virtual network and subnet toocreate network interfaces:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

<span data-ttu-id="6cf43-159">Spowoduje to utworzenie interfejsu sieciowego, który należy puli zaplecza modułu równoważenia obciążenia toohello i skojarzyć hello pierwszej reguły NAT dla protokołu RDP dla tego interfejsu sieci:</span><span class="sxs-lookup"><span data-stu-id="6cf43-159">This step creates a network interface which will belong toohello load balancer back end pool and associate hello first NAT rule for RDP for this network interface:</span></span>

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a><span data-ttu-id="6cf43-160">Krok 2</span><span class="sxs-lookup"><span data-stu-id="6cf43-160">Step 2</span></span>

<span data-ttu-id="6cf43-161">Utwórz drugi interfejs sieciowej o nazwie LB-Nic2-BE:</span><span class="sxs-lookup"><span data-stu-id="6cf43-161">Create a second network interface called LB-Nic2-BE:</span></span>

<span data-ttu-id="6cf43-162">Spowoduje to utworzenie drugiego interfejsu sieciowego, przypisywanie toohello tego samego modułu równoważenia obciążenia ponownie kończyć puli i kojarzenie hello drugą regułę NAT utworzone dla protokołu RDP:</span><span class="sxs-lookup"><span data-stu-id="6cf43-162">This step creates a second network interface, assigning toohello same load balancer back end pool and associating hello second NAT rule created for RDP:</span></span>

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

<span data-ttu-id="6cf43-163">wynik końcowy Hello zostaną wyświetlone następujące hello:</span><span class="sxs-lookup"><span data-stu-id="6cf43-163">hello end result will show hello following:</span></span>

    $backendnic1

<span data-ttu-id="6cf43-164">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="6cf43-164">Expected output:</span></span>

    Name                 : lb-nic1-be
    ResourceGroupName    : NRP-RG
    Location             : westus
    Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
    Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
    ProvisioningState    : Succeeded
    Tags                 :
    VirtualMachine       : null
    IpConfigurations     : [
                         {
                           "PrivateIpAddress": "10.0.2.6",
                           "PrivateIpAllocationMethod": "Static",
                           "Subnet": {
                             "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                           },
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
                           "ProvisioningState": "Succeeded",
                           "Name": "ipconfig1",
                           "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                           "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1"
                         }
                       ]
    DnsSettings          : {
                         "DnsServers": [],
                         "AppliedDnsServers": []
                       }
    AppliedDnsSettings   :
    NetworkSecurityGroup : null
    Primary              : False



### <a name="step-3"></a><span data-ttu-id="6cf43-165">Krok 3</span><span class="sxs-lookup"><span data-stu-id="6cf43-165">Step 3</span></span>

<span data-ttu-id="6cf43-166">Użyj hello polecenia Add-AzureRmVMNetworkInterface tooassign hello kart tooa wirtualnej komputera.</span><span class="sxs-lookup"><span data-stu-id="6cf43-166">Use hello command Add-AzureRmVMNetworkInterface tooassign hello NIC tooa virtual Machine.</span></span>

<span data-ttu-id="6cf43-167">Witaj toocreate instrukcje krok po kroku maszynę wirtualną i przypisać tooa kart interfejsu Sieciowego można znaleźć następującej dokumentacji hello: [tworzenia maszyny Wirtualnej platformy Azure przy użyciu programu PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6cf43-167">You can find hello step by step instructions toocreate a virtual machine and assign tooa NIC following hello documentation: [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-hello-network-interface"></a><span data-ttu-id="6cf43-168">Dodaj hello interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="6cf43-168">Add hello network interface</span></span>

<span data-ttu-id="6cf43-169">Jeśli masz już maszyny wirtualnej utworzonej, można dodać hello interfejsu sieciowego z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6cf43-169">If you already have a virtual machine created, you can add hello network interface with hello following steps:</span></span>

### <a name="step-1"></a><span data-ttu-id="6cf43-170">Krok 1</span><span class="sxs-lookup"><span data-stu-id="6cf43-170">Step 1</span></span>

<span data-ttu-id="6cf43-171">Ładowanie zasobów usługi równoważenia obciążenia hello do zmiennej (Jeśli użytkownik jeszcze nie).</span><span class="sxs-lookup"><span data-stu-id="6cf43-171">Load hello load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="6cf43-172">Zmienna Hello używana jest $lb o nazwie i powitalne użycia tych samych nazw z zasobu usługi równoważenia obciążenia hello utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="6cf43-172">hello variable used is called $lb and use hello same names from hello load balancer resource created above.</span></span>

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="6cf43-173">Krok 2</span><span class="sxs-lookup"><span data-stu-id="6cf43-173">Step 2</span></span>

<span data-ttu-id="6cf43-174">Zmienna tooa obciążenia hello wewnętrznej bazy danych konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="6cf43-174">Load hello backend configuration tooa variable.</span></span>

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a><span data-ttu-id="6cf43-175">Krok 3</span><span class="sxs-lookup"><span data-stu-id="6cf43-175">Step 3</span></span>

<span data-ttu-id="6cf43-176">Załaduj hello już utworzone, interfejs sieciowy do zmiennej.</span><span class="sxs-lookup"><span data-stu-id="6cf43-176">Load hello already created network interface into a variable.</span></span> <span data-ttu-id="6cf43-177">Nazwa zmiennej Hello używana jest $ karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="6cf43-177">hello variable name used is $nic.</span></span> <span data-ttu-id="6cf43-178">Nazwa interfejsu sieciowego Hello używany jest sama hello w powyższym przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="6cf43-178">hello network interface name used is hello same from hello example above.</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a><span data-ttu-id="6cf43-179">Krok 4</span><span class="sxs-lookup"><span data-stu-id="6cf43-179">Step 4</span></span>

<span data-ttu-id="6cf43-180">Zmień konfigurację zaplecza hello na powitania interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="6cf43-180">Change hello backend configuration on hello network interface.</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a><span data-ttu-id="6cf43-181">Krok 5</span><span class="sxs-lookup"><span data-stu-id="6cf43-181">Step 5</span></span>

<span data-ttu-id="6cf43-182">Zapisz obiekt interfejsu sieciowego hello.</span><span class="sxs-lookup"><span data-stu-id="6cf43-182">Save hello network interface object.</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="6cf43-183">Po dodaniu interfejsu sieciowego puli zaplecza modułu równoważenia obciążenia toohello uruchamia odbieranie ruchu sieciowego oparte na reguł dla tego zasobu usługi równoważenia obciążenia równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="6cf43-183">After a network interface is added toohello load balancer backend pool, it starts receiving network traffic based on hello load balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="6cf43-184">Aktualizowanie istniejącego modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="6cf43-184">Update an existing load balancer</span></span>

### <a name="step-1"></a><span data-ttu-id="6cf43-185">Krok 1</span><span class="sxs-lookup"><span data-stu-id="6cf43-185">Step 1</span></span>
<span data-ttu-id="6cf43-186">Przy użyciu usługi równoważenia obciążenia hello w powyższym przykładzie hello, przypisz toovariable obiekt usługi równoważenia obciążenia przy użyciu Get-AzureRmLoadBalancer $slb</span><span class="sxs-lookup"><span data-stu-id="6cf43-186">Using hello load balancer from hello example above, assign load balancer object toovariable $slb using Get-AzureRmLoadBalancer</span></span>

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="6cf43-187">Krok 2</span><span class="sxs-lookup"><span data-stu-id="6cf43-187">Step 2</span></span>

<span data-ttu-id="6cf43-188">W hello poniższy przykład spowoduje dodanie nowej reguły ruchu przychodzącego translatora adresów Sieciowych przy użyciu portu 81 hello frontonu i portu 8181 kopia hello kończyć puli tooan istniejący moduł równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="6cf43-188">In hello following example, you will add a new Inbound NAT rule using port 81 in hello front end and port 8181 for hello back end pool tooan existing load balancer</span></span>

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a><span data-ttu-id="6cf43-189">Krok 3</span><span class="sxs-lookup"><span data-stu-id="6cf43-189">Step 3</span></span>

<span data-ttu-id="6cf43-190">Zapisz nową konfigurację hello przy użyciu zestawu AzureLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="6cf43-190">Save hello new configuration using Set-AzureLoadBalancer</span></span>

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="6cf43-191">Usuwanie modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="6cf43-191">Remove a load balancer</span></span>

<span data-ttu-id="6cf43-192">Użyj hello polecenia Remove-AzureRmLoadBalancer toodelete modułu równoważenia obciążenia utworzonej wcześniej o nazwie "Dostawca NRP-LB" w grupie zasobów o nazwie "Zarządcy zasobów NRP"</span><span class="sxs-lookup"><span data-stu-id="6cf43-192">Use hello command Remove-AzureRmLoadBalancer toodelete a previously created load balancer named "NRP-LB"  in a resource group called "NRP-RG"</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="6cf43-193">Można opcjonalnie hello przełącznika - Force tooavoid hello wiersza do usunięcia.</span><span class="sxs-lookup"><span data-stu-id="6cf43-193">You can use hello optional switch -Force tooavoid hello prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6cf43-194">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6cf43-194">Next steps</span></span>

<span data-ttu-id="6cf43-195">[Configure a Load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="6cf43-195">[Configure a Load balancer distribution mode](load-balancer-distribution-mode.md)</span></span>

<span data-ttu-id="6cf43-196">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="6cf43-196">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md)</span></span>
