---
title: "Ustawia aaaCreating skalowania maszyn wirtualnych przy użyciu poleceń cmdlet programu PowerShell | Dokumentacja firmy Microsoft"
description: "Rozpocząć tworzenie i zarządzanie nimi z pierwszego zestawy skalowania maszyny wirtualnej Azure, na przy użyciu poleceń cmdlet programu Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 430d9d64-1f35-48f0-a4fd-9b69910ffa59
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: danielsollondon
ms.openlocfilehash: 7979be367d04c904b60d78849c1b751a52cc8caf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-virtual-machine-scale-sets-using-powershell-cmdlets"></a><span data-ttu-id="46831-103">Tworzenie zestawów skali maszyny wirtualnej za pomocą poleceń cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="46831-103">Creating Virtual Machine Scale Sets using PowerShell cmdlets</span></span>
<span data-ttu-id="46831-104">W tym artykule przedstawiono przykład sposobu toocreate zestawu skalowania maszyn wirtualnych (VMSS).</span><span class="sxs-lookup"><span data-stu-id="46831-104">This article walks through an example of how toocreate a Virtual Machine scale set (VMSS).</span></span> <span data-ttu-id="46831-105">Tworzy zestaw skalowania trzy węzły z skojarzone sieci i magazynu.</span><span class="sxs-lookup"><span data-stu-id="46831-105">It creates a scale set of three nodes, with associated Networking and Storage.</span></span>

## <a name="first-steps"></a><span data-ttu-id="46831-106">Pierwsze kroki</span><span class="sxs-lookup"><span data-stu-id="46831-106">First Steps</span></span>
<span data-ttu-id="46831-107">Upewnij się, masz hello zainstalowane najnowsze modułu Azure PowerShell, toomake upewnić się, że polecenia cmdlet środowiska PowerShell hello potrzeby toomaintain i utworzyć zestawy skalowania.</span><span class="sxs-lookup"><span data-stu-id="46831-107">Ensure you have hello latest Azure PowerShell module installed, toomake sure you have hello PowerShell commandlets needed toomaintain, and create scale sets.</span></span>
<span data-ttu-id="46831-108">Przejdź do narzędzia wiersza polecenia toohello [tutaj](http://aka.ms/webpi-azps) dla hello najnowszych dostępnych modułów Azure.</span><span class="sxs-lookup"><span data-stu-id="46831-108">Go toohello command line tools [here](http://aka.ms/webpi-azps) for hello latest available Azure Modules.</span></span>

<span data-ttu-id="46831-109">polecenia cmdlet związane z toofind VMSS, użyj ciągu wyszukiwania hello \*VMSS\*.</span><span class="sxs-lookup"><span data-stu-id="46831-109">toofind VMSS related commandlets, use hello search string \*VMSS\*.</span></span> <span data-ttu-id="46831-110">Na przykład _gcm *vmss*_</span><span class="sxs-lookup"><span data-stu-id="46831-110">For example, _gcm *vmss*_</span></span>

## <a name="creating-a-vmss"></a><span data-ttu-id="46831-111">Tworzenie VMSS</span><span class="sxs-lookup"><span data-stu-id="46831-111">Creating a VMSS</span></span>
#### <a name="create-resource-group"></a><span data-ttu-id="46831-112">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="46831-112">Create Resource Group</span></span>
```
$loc = 'westus';
$rgname = 'mynewrgwu';
  New-AzureRmResourceGroup -Name $rgname -Location $loc -Force;
```

### <a name="create-networking-vnet--subnet"></a><span data-ttu-id="46831-113">Tworzenie sieci (Wirtualnej / podsieci)</span><span class="sxs-lookup"><span data-stu-id="46831-113">Create Networking (VNET / Subnet)</span></span>
#### <a name="subnet-specification"></a><span data-ttu-id="46831-114">Specyfikacja podsieci</span><span class="sxs-lookup"><span data-stu-id="46831-114">Subnet Specification</span></span>
```
$subnetName = 'websubnet'
  $subnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix "10.0.0.0/24";
```

#### <a name="vnet-specification"></a><span data-ttu-id="46831-115">Specyfikacja sieci Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="46831-115">VNET Specification</span></span>
```
$vnet = New-AzureRmVirtualNetwork -Force -Name ('vnet' + $rgname) -ResourceGroupName $rgname -Location $loc -AddressPrefix "10.0.0.0/16" -Subnet $subnet;
$vnet = Get-AzureRmVirtualNetwork -Name ('vnet' + $rgname) -ResourceGroupName $rgname;

# In this case assume hello new subnet is hello only one
$subnetId = $vnet.Subnets[0].Id;
```

#### <a name="create-public-ip-resource-tooallow-external-access"></a><span data-ttu-id="46831-116">Tworzenie publicznego adresu IP zasobu tooAllow dostępu zewnętrznego</span><span class="sxs-lookup"><span data-stu-id="46831-116">Create Public IP Resource tooAllow External Access</span></span>
<span data-ttu-id="46831-117">Są to toohello powiązanej usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="46831-117">This will be bound toohello Load Balancer.</span></span>

```
$pubip = New-AzureRmPublicIpAddress -Force -Name ('pubip' + $rgname) -ResourceGroupName $rgname -Location $loc -AllocationMethod Dynamic -DomainNameLabel ('pubip' + $rgname);
$pubip = Get-AzureRmPublicIpAddress -Name ('pubip' + $rgname) -ResourceGroupName $rgname;
```

#### <a name="create-load-balancer"></a><span data-ttu-id="46831-118">Tworzenie usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="46831-118">Create Load Balancer</span></span>
```
$frontendName = 'fe' + $rgname
$backendAddressPoolName = 'bepool' + $rgname
$probeName = 'vmssprobe' + $rgname
$inboundNatPoolName = 'innatpool' + $rgname
$lbruleName = 'lbrule' + $rgname
$lbName = 'vmsslb' + $rgname

# Bind Public IP tooLoad Balancer
$frontend = New-AzureRmLoadBalancerFrontendIpConfig -Name $frontendName -PublicIpAddress $pubip
```

#### <a name="configure-load-balancer"></a><span data-ttu-id="46831-119">Konfigurowanie usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="46831-119">Configure Load Balancer</span></span>
<span data-ttu-id="46831-120">Tworzenie konfiguracji puli adresów zaplecza, to będzie udostępniany przez karty sieciowe hello hello maszyn wirtualnych w zestawie skalowania hello.</span><span class="sxs-lookup"><span data-stu-id="46831-120">Create Backend Address Pool Config, this will be shared by hello NICs of hello VMs in hello scale set.</span></span>

```
$backendAddressPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name $backendAddressPoolName
```

<span data-ttu-id="46831-121">Ustawiony Port sondy z równoważeniem obciążenia, Zmień ustawienia hello odpowiedni dla twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="46831-121">Set Load Balanced Probe Port, change hello settings as appropriate for your application.</span></span>

```
$probe = New-AzureRmLoadBalancerProbeConfig -Name $probeName -RequestPath healthcheck.aspx -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
```

<span data-ttu-id="46831-122">Tworzenie puli NAT dla ruchu przychodzącego bezpośrednie połączenie między kierowanymi (zrównoważonym obciążeniu) toohello maszyn wirtualnych w skali hello ustawionych wcześniej za pośrednictwem hello moduł równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="46831-122">Create an inbound NAT pool for direct routed connectivity (not load balanced) toohello VMs in hello scale set via hello Load Balancer.</span></span> <span data-ttu-id="46831-123">To jest toodemonstrate za pomocą protokołu RDP i nie mogą być wymagane w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="46831-123">This is toodemonstrate using RDP and may not be required in your application.</span></span>

```
$frontendpoolrangestart = 3360
$frontendpoolrangeend = 3370
$backendvmport = 3389
$inboundNatPool = New-AzureRmLoadBalancerInboundNatPoolConfig -Name $inboundNatPoolName -FrontendIPConfigurationId `
$frontend.Id -Protocol Tcp -FrontendPortRangeStart $frontendpoolrangestart -FrontendPortRangeEnd $frontendpoolrangeend -BackendPort $backendvmport;
```

<span data-ttu-id="46831-124">Utwórz hello załadować zrównoważonym reguły w przykładzie przedstawiono załadować równoważenia port 80 żądań, przy użyciu ustawień hello z poprzednich kroków.</span><span class="sxs-lookup"><span data-stu-id="46831-124">Create hello Load Balanced Rule, this example shows load balancing port 80 requests, using hello settings from previous steps.</span></span>

```
$protocol = 'Tcp'
$feLBPort = 80
$beLBPort = 80

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name $lbruleName `
-FrontendIPConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -Protocol $protocol -FrontendPort $feLBPort -BackendPort $beLBPort `
-IdleTimeoutInMinutes 15 -EnableFloatingIP -LoadDistribution SourceIP -Verbose;
```

<span data-ttu-id="46831-125">Utwórz moduł równoważenia obciążenia w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="46831-125">Create Load Balancer with configuration.</span></span>

```
$actualLb = New-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname -Location $loc `
-FrontendIpConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -LoadBalancingRule $lbrule -InboundNatPool $inboundNatPool -Verbose;
```

<span data-ttu-id="46831-126">Sprawdź ustawienia LB, sprawdź obciążenia configs zrównoważonym portów, należy zwrócić uwagę, nie będzie mógł przeglądać reguły NAT ruchu przychodzącego do hello maszyn wirtualnych w zestawie skalowania hello są tworzone.</span><span class="sxs-lookup"><span data-stu-id="46831-126">Check  LB settings, check load balanced port configs, note, you will not see Inbound NAT rules until hello VMs in hello scale set are created.</span></span>

```
$expectedLb = Get-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname
```

##### <a name="configure-and-create-hello-scale-set"></a><span data-ttu-id="46831-127">Skonfigurowania i Utwórz hello skali</span><span class="sxs-lookup"><span data-stu-id="46831-127">Configure and Create hello scale set</span></span>
<span data-ttu-id="46831-128">Uwaga: w tym przykładzie infrastruktury pokazano sposób dystrybucji tooset w górę i skalowania ruchu w sieci web przez zestaw skali hello, ale hello obrazów maszyn wirtualnych określone w tym miejscu nie mają żadnych zainstalowanych usług sieci web.</span><span class="sxs-lookup"><span data-stu-id="46831-128">Note, this infrastructure example shows how tooset up distribute and scale web traffic across hello scale set, but hello VMs Images specified here do not have any web services installed.</span></span>

```
# specify scale set Name
$vmssName = 'vmss' + $rgname;

## specify VMSS specific details
$adminUsername = 'azadmin';
$adminPassword = "Password1234!";

$PublisherName = 'MicrosoftWindowsServer'
$Offer         = 'WindowsServer'
$Sku          = '2012-R2-Datacenter'
$Version       = 'latest'
$vmNamePrefix = 'winvmss'

###add an extension
$extname = 'BGInfo';
$publisher = 'Microsoft.Compute';
$exttype = 'BGInfo';
$extver = '2.1';
```

<span data-ttu-id="46831-129">Powiąż tooLoad karta sieciowa usługi równoważenia i podsieci</span><span class="sxs-lookup"><span data-stu-id="46831-129">Bind NIC tooLoad Balancer and Subnet</span></span>

```
$ipCfg = New-AzureRmVmssIPConfig -Name 'nic' `
-LoadBalancerInboundNatPoolsId $actualLb.InboundNatPools[0].Id `
-LoadBalancerBackendAddressPoolsId $actualLb.BackendAddressPools[0].Id `
-SubnetId $subnetId;
```

<span data-ttu-id="46831-130">Utwórz skali set Config</span><span class="sxs-lookup"><span data-stu-id="46831-130">Create scale set Config</span></span>

```
# Specify number of nodes
$numberofnodes = 3

$vmss = New-AzureRmVmssConfig -Location $loc -SkuCapacity $numberofnodes -SkuName 'Standard_A2' -UpgradePolicyMode 'automatic' `
    | Add-AzureRmVmssNetworkInterfaceConfiguration -Name $subnetName -Primary $true -IPConfiguration $ipCfg `
    | Set-AzureRmVmssOSProfile -ComputerNamePrefix $vmNamePrefix -AdminUsername $adminUsername -AdminPassword $adminPassword `
    | Set-AzureRmVmssStorageProfile -OsDiskCreateOption 'FromImage' -OsDiskCaching 'None' `
    -ImageReferenceOffer $Offer -ImageReferenceSku $Sku -ImageReferenceVersion $Version `
    -ImageReferencePublisher $PublisherName `
    | Add-AzureRmVmssExtension -Name $extname -Publisher $publisher -Type $exttype -TypeHandlerVersion $extver -AutoUpgradeMinorVersion $true
```

<span data-ttu-id="46831-131">Konfiguracja zestawu skali kompilacji</span><span class="sxs-lookup"><span data-stu-id="46831-131">Build scale set configuration</span></span>

```
New-AzureRmVmss -ResourceGroupName $rgname -Name $vmssName -VirtualMachineScaleSet $vmss -Verbose;
```

<span data-ttu-id="46831-132">Zestaw skali hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="46831-132">Now you have created hello scale set.</span></span> <span data-ttu-id="46831-133">Można przetestować połączenia toohello poszczególnych maszyn wirtualnych za pomocą protokołu RDP w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="46831-133">You can test connecting toohello individual VM using RDP in this example:</span></span>

```
VM0 : pubipmynewrgwu.westus.cloudapp.azure.com:3360
VM1 : pubipmynewrgwu.westus.cloudapp.azure.com:3361
VM2 : pubipmynewrgwu.westus.cloudapp.azure.com:3362
```
