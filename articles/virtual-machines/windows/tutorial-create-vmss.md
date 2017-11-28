---
title: "aaaCreate maszyny wirtualnej skali zestawów dla systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie i wdrażanie aplikacji wysokiej dostępności na maszynach wirtualnych z systemem Windows przy użyciu zestawu skali maszyny wirtualnej"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: 
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: a3914571005c28a492c069d880992630851afae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a><span data-ttu-id="bd846-103">Tworzenie zestawu skalowania maszyny wirtualnej i wdrażanie wysokiej dostępności aplikacji w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="bd846-103">Create a Virtual Machine Scale Set and deploy a highly available app on Windows</span></span>
<span data-ttu-id="bd846-104">Zestaw skali maszyny wirtualnej umożliwia toodeploy i zarządzać zestawem identyczne, automatyczne skalowanie maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="bd846-104">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="bd846-105">Można ręcznie skalować hello liczbę maszyn wirtualnych w zestawie skalowania hello lub zdefiniuj tooautoscale reguły na podstawie użycia procesora CPU, pamięci żądanie lub ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="bd846-105">You can scale hello number of VMs in hello scale set manually, or define rules tooautoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="bd846-106">W tym samouczku możesz wdrożyć skali maszyny wirtualnej w usłudze Azure.</span><span class="sxs-lookup"><span data-stu-id="bd846-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="bd846-107">Omawiane kwestie:</span><span class="sxs-lookup"><span data-stu-id="bd846-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bd846-108">Użyj hello niestandardowe rozszerzenie skryptu toodefine tooscale witryny usług IIS</span><span class="sxs-lookup"><span data-stu-id="bd846-108">Use hello Custom Script Extension toodefine an IIS site tooscale</span></span>
> * <span data-ttu-id="bd846-109">Tworzenie modułu równoważenia obciążenia dla zestawu skalowania</span><span class="sxs-lookup"><span data-stu-id="bd846-109">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="bd846-110">Utwórz zestaw skali maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="bd846-110">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="bd846-111">Zwiększanie lub zmniejszanie hello liczbę wystąpień w zestawie skalowania</span><span class="sxs-lookup"><span data-stu-id="bd846-111">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="bd846-112">Tworzenie reguł skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="bd846-112">Create autoscale rules</span></span>

<span data-ttu-id="bd846-113">Ten samouczek wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="bd846-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="bd846-114">Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="bd846-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="bd846-115">Jeśli potrzebujesz tooupgrade, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="bd846-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="scale-set-overview"></a><span data-ttu-id="bd846-116">Omówienie zestawu skali</span><span class="sxs-lookup"><span data-stu-id="bd846-116">Scale Set overview</span></span>
<span data-ttu-id="bd846-117">Zestawy skalowania używać podobne pojęcia poznanie w samouczku poprzedniej hello zbyt[tworzyć maszyny wirtualne o wysokiej dostępności](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="bd846-117">Scale sets use similar concepts as you learned about in hello previous tutorial too[Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="bd846-118">Maszyny wirtualne w zestawie skalowania są dystrybuowane między domenami usterek i aktualizacji, podobnie jak maszyn wirtualnych w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="bd846-118">VMs in a scale set are distributed across fault and update domains just like VMs in an availability set.</span></span>

<span data-ttu-id="bd846-119">Maszyny wirtualne są tworzone zgodnie z potrzebami w zestawie skalowania.</span><span class="sxs-lookup"><span data-stu-id="bd846-119">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="bd846-120">Zdefiniuj toocontrol reguł skalowania automatycznego, kiedy maszyny wirtualne są dodawane lub usuwane z hello zestaw skali.</span><span class="sxs-lookup"><span data-stu-id="bd846-120">You define autoscale rules toocontrol how and when VMs are added or removed from hello scale set.</span></span> <span data-ttu-id="bd846-121">Te reguły może wyzwolić na podstawie metryk, takich jak obciążenie procesora CPU, pamięć lub ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="bd846-121">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="bd846-122">Obsługa się too1, 000 maszyn wirtualnych, gdy używasz obrazu platformy Azure zestawach skali.</span><span class="sxs-lookup"><span data-stu-id="bd846-122">Scale sets support up too1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="bd846-123">W przypadku obciążeń z instalacją znaczących lub wymagania dotyczące dostosowywania maszyny Wirtualnej, możesz za[utworzyć niestandardowy obraz maszyny Wirtualnej](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="bd846-123">For workloads with significant installation or VM customization requirements, you may wish too[Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="bd846-124">Możesz utworzyć zapasowych maszyn wirtualnych too100 w skali ustawić przy użyciu obrazu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="bd846-124">You can create up too100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-tooscale"></a><span data-ttu-id="bd846-125">Utwórz tooscale aplikacji</span><span class="sxs-lookup"><span data-stu-id="bd846-125">Create an app tooscale</span></span>
<span data-ttu-id="bd846-126">Przed utworzeniem zestaw skali, Utwórz grupę zasobów o [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="bd846-126">Before you can create a scale set, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="bd846-127">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupAutomate* w hello *EastUS* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="bd846-127">hello following example creates a resource group named *myResourceGroupAutomate* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

<span data-ttu-id="bd846-128">W starszych samouczka przedstawiono sposób zbyt[konfiguracji zautomatyzować maszyny Wirtualnej](tutorial-automate-vm-deployment.md) przy użyciu hello niestandardowe rozszerzenie skryptu.</span><span class="sxs-lookup"><span data-stu-id="bd846-128">In an earlier tutorial, you learned how too[Automate VM configuration](tutorial-automate-vm-deployment.md) using hello Custom Script Extension.</span></span> <span data-ttu-id="bd846-129">Utwórz konfigurację zestaw skali, a następnie Zastosuj tooinstall niestandardowe rozszerzenie skryptu i skonfigurować usługi IIS:</span><span class="sxs-lookup"><span data-stu-id="bd846-129">Create a scale set configuration then apply a Custom Script Extension tooinstall and configure IIS:</span></span>

```powershell
# Create a config object
$vmssConfig = New-AzureRmVmssConfig `
    -Location EastUS `
    -SkuCapacity 2 `
    -SkuName Standard_DS2 `
    -UpgradePolicyMode Automatic

# Define hello script for your Custom Script Extension toorun
$publicSettings = @{
    "fileUris" = (,"https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate-iis.ps1");
    "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File automate-iis.ps1"
}

# Use Custom Script Extension tooinstall IIS and configure basic website
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig `
    -Name "customScript" `
    -Publisher "Microsoft.Compute" `
    -Type "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -Setting $publicSettings
```

## <a name="create-scale-load-balancer"></a><span data-ttu-id="bd846-130">Tworzenie usługi równoważenia obciążenia skali</span><span class="sxs-lookup"><span data-stu-id="bd846-130">Create scale load balancer</span></span>
<span data-ttu-id="bd846-131">Moduł równoważenia obciążenia Azure jest równoważenia obciążenia warstwy 4 (TCP, UDP), który zapewnia wysoką dostępność, przekazując przychodzący ruch między maszynami wirtualnymi w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="bd846-131">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="bd846-132">Kondycji sondę modułu równoważenia obciążenia monitoruje danego portu na każdej maszynie Wirtualnej, a tylko dystrybuuje ruch tooan operacyjne maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bd846-132">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span> <span data-ttu-id="bd846-133">Aby uzyskać więcej informacji, zobacz następny samouczek hello na [jak tooload złoty środek między maszynami wirtualnymi systemu Windows](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="bd846-133">For more information, see hello next tutorial on [How tooload balance Windows virtual machines](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="bd846-134">Utwórz moduł równoważenia obciążenia, który ma publicznego adresu IP i rozpowszechnia ruchu w sieci web na porcie 80:</span><span class="sxs-lookup"><span data-stu-id="bd846-134">Create a load balancer that has a public IP address and distributes web traffic on port 80:</span></span>

```powershell
# Create a public IP address
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupScaleSet `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP

# Create a frontend and backend IP pool
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool

# Create hello load balancer
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool

# Create a load balancer health probe on port 80
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2

# Create a load balancer rule toodistribute traffic on port 80
Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80

# Update hello load balancer configuration
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="create-a-scale-set"></a><span data-ttu-id="bd846-135">Utwórz zestaw skali</span><span class="sxs-lookup"><span data-stu-id="bd846-135">Create a scale set</span></span>
<span data-ttu-id="bd846-136">Teraz Utwórz zestaw o skali maszyny wirtualnej [AzureRmVmss nowy](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="bd846-136">Now create a virtual machine scale set with [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="bd846-137">Witaj poniższy przykład tworzy zestaw o nazwie skalowania *myScaleSet*:</span><span class="sxs-lookup"><span data-stu-id="bd846-137">hello following example creates a scale set named *myScaleSet*:</span></span>

```powershell
# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig `
  -ImageReferencePublisher MicrosoftWindowsServer `
  -ImageReferenceOffer WindowsServer `
  -ImageReferenceSku 2016-Datacenter `
  -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig `
  -AdminUsername azureuser `
  -AdminPassword P@ssword! `
  -ComputerNamePrefix myVM

# Create hello virtual network resources
$subnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name "mySubnet" `
  -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName "myResourceGroupScaleSet" `
  -Name "myVnet" `
  -Location "EastUS" `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $subnet
$ipConfig = New-AzureRmVmssIpConfig `
  -Name "myIPConfig" `
  -LoadBalancerBackendAddressPoolsId $lb.BackendAddressPools[0].Id `
  -SubnetId $vnet.Subnets[0].Id

# Attach hello virtual network toohello config object
Add-AzureRmVmssNetworkInterfaceConfiguration `
  -VirtualMachineScaleSet $vmssConfig `
  -Name "network-config" `
  -Primary $true `
  -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myScaleSet `
  -VirtualMachineScaleSet $vmssConfig
```

<span data-ttu-id="bd846-138">Go zajmuje kilka minut toocreate i skonfiguruje wszystkie zasoby zestaw skalowania hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="bd846-138">It takes a few minutes toocreate and configure all hello scale set resources and VMs.</span></span>


## <a name="test-your-app"></a><span data-ttu-id="bd846-139">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="bd846-139">Test your app</span></span>
<span data-ttu-id="bd846-140">toosee witryny sieci Web programu IIS w akcji, Uzyskaj hello publicznego adresu IP z usługi równoważenia obciążenia z [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="bd846-140">toosee your IIS website in action, obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="bd846-141">Witaj poniższy przykład uzyskuje hello adres IP dla *myPublicIP* utworzone jako część zestawu skalowania hello:</span><span class="sxs-lookup"><span data-stu-id="bd846-141">hello following example obtains hello IP address for *myPublicIP* created as part of hello scale set:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

<span data-ttu-id="bd846-142">Wprowadź hello publicznego adresu IP w przeglądarce sieci web tooa.</span><span class="sxs-lookup"><span data-stu-id="bd846-142">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="bd846-143">Aplikacja Hello jest wyświetlana, łącznie z nazwą hosta hello hello hello tej maszyny Wirtualnej obciążenia ruchu równoważenia dystrybuowane do:</span><span class="sxs-lookup"><span data-stu-id="bd846-143">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic to:</span></span>

![Uruchomionej witryny usług IIS](./media/tutorial-create-vmss/running-iis-site.png)

<span data-ttu-id="bd846-145">zestaw w akcji skalowania hello toosee, możesz można życie odświeżania obciążenia hello toosee przeglądarki sieci web równoważenia rozpowszechniają wszystkich aplikacji uruchomionych maszyn wirtualnych hello ruchu.</span><span class="sxs-lookup"><span data-stu-id="bd846-145">toosee hello scale set in action, you can force-refresh your web browser toosee hello load balancer distribute traffic across all hello VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="bd846-146">Zadania zarządzania</span><span class="sxs-lookup"><span data-stu-id="bd846-146">Management tasks</span></span>
<span data-ttu-id="bd846-147">W całym cyklu życia hello zestawu skali hello, może być konieczne toorun jednego lub więcej zadań zarządzania.</span><span class="sxs-lookup"><span data-stu-id="bd846-147">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="bd846-148">Ponadto można toocreate skrypty, które automatyzacji różnych zadań cyklu życia.</span><span class="sxs-lookup"><span data-stu-id="bd846-148">Additionally, you may want toocreate scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="bd846-149">Program Azure PowerShell udostępnia toodo szybko tych zadań.</span><span class="sxs-lookup"><span data-stu-id="bd846-149">Azure PowerShell provides a quick way toodo those tasks.</span></span> <span data-ttu-id="bd846-150">Poniżej przedstawiono kilka typowych zadań.</span><span class="sxs-lookup"><span data-stu-id="bd846-150">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="bd846-151">Maszyny wirtualne widoku w zestawie skalowania</span><span class="sxs-lookup"><span data-stu-id="bd846-151">View VMs in a scale set</span></span>
<span data-ttu-id="bd846-152">Ustaw listę maszyn wirtualnych uruchomionych w skali sieci tooview, użyj [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="bd846-152">tooview a list of VMs running in your scale set, use [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) as follows:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Loop through hello instanaces in your scale set
for ($i=1; $i -le ($scaleset.Sku.Capacity - 1); $i++) {
    Get-AzureRmVmssVM -ResourceGroupName myResourceGroupScaleSet `
      -VMScaleSetName myScaleSet `
      -InstanceId $i
}
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="bd846-153">Zwiększanie lub zmniejszanie wystąpień maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="bd846-153">Increase or decrease VM instances</span></span>
<span data-ttu-id="bd846-154">toosee hello liczbę wystąpień obecnie w skali ustawiono, użyj [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) i wykonywać zapytania na *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="bd846-154">toosee hello number of instances you currently have in a scale set, use [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) and query on *sku.capacity*:</span></span>

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

<span data-ttu-id="bd846-155">Możesz ręcznie zwiększyć lub zmniejszyć liczbę hello maszyn wirtualnych w skali hello ustawiony za pomocą [AzureRmVmss aktualizacji](/powershell/module/azurerm.compute/update-azurermvmss).</span><span class="sxs-lookup"><span data-stu-id="bd846-155">You can then manually increase or decrease hello number of virtual machines in hello scale set with [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss).</span></span> <span data-ttu-id="bd846-156">Witaj poniższy przykład przedstawia hello liczbę maszyn wirtualnych w sieci za zestaw skalowania*5*:</span><span class="sxs-lookup"><span data-stu-id="bd846-156">hello following example sets hello number of VMs in your scale set too*5*:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Set and update hello capacity of your scale set
$scaleset.sku.capacity = 5
Update-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -Name myScaleSet `
    -VirtualMachineScaleSet $scaleset
```

<span data-ttu-id="bd846-157">Jeśli zajmuje kilka minut tooupdate hello określona liczba wystąpień w zestawie skali.</span><span class="sxs-lookup"><span data-stu-id="bd846-157">If takes a few minutes tooupdate hello specified number of instances in your scale set.</span></span>


### <a name="configure-autoscale-rules"></a><span data-ttu-id="bd846-158">Konfigurowanie reguł automatycznego skalowania</span><span class="sxs-lookup"><span data-stu-id="bd846-158">Configure autoscale rules</span></span>
<span data-ttu-id="bd846-159">Zamiast ręcznie skalowania hello liczbę wystąpień w skali sieci, należy zdefiniować regułę automatycznego skalowania.</span><span class="sxs-lookup"><span data-stu-id="bd846-159">Rather than manually scaling hello number of instances in your scale set, you define autoscale rules.</span></span> <span data-ttu-id="bd846-160">Te reguły monitorować hello wystąpień w skali sieci ustawić i odpowiedzi, w związku z tym na podstawie metryk i progów, które należy zdefiniować.</span><span class="sxs-lookup"><span data-stu-id="bd846-160">These rules monitor hello instances in your scale set and respond accordingly based on metrics and thresholds you define.</span></span> <span data-ttu-id="bd846-161">Poniższy przykład Hello skaluje hello liczbę wystąpień przez jedną gdy obciążenie procesora CPU średni hello jest większy niż 60% w okresie 5 minut.</span><span class="sxs-lookup"><span data-stu-id="bd846-161">hello following example scales out hello number of instances by one when hello average CPU load is greater than 60% over a 5 minute period.</span></span> <span data-ttu-id="bd846-162">Jeśli w okresie 5 minut obciążenia procesora CPU średnia hello spadnie poniżej 30%, wystąpień hello są skalowane w przez jedno wystąpienie:</span><span class="sxs-lookup"><span data-stu-id="bd846-162">If hello average CPU load then drops below 30% over a 5 minute period, hello instances are scaled in by one instance:</span></span>

```powershell
# Define your scale set information
$mySubscriptionId = (Get-AzureRmSubscription).Id
$myResourceGroup = "myResourceGroupScaleSet"
$myScaleSet = "myScaleSet"
$myLocation = "East US"

# Create a scale up rule tooincrease hello number instances after 60% average CPU usage exceeded for a 5 minute period
$myRuleScaleUp = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator GreaterThan `
  -MetricStatistic Average `
  -Threshold 60 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Increase `
  -ScaleActionValue 1

# Create a scale down rule toodecrease hello number of instances after 30% average CPU usage over a 5 minute period
$myRuleScaleDown = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator LessThan `
  -MetricStatistic Average `
  -Threshold 30 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Decrease `
  -ScaleActionValue 1

# Create a scale profile with your scale up and scale down rules
$myScaleProfile = New-AzureRmAutoscaleProfile `
  -DefaultCapacity 2  `
  -MaximumCapacity 10 `
  -MinimumCapacity 2 `
  -Rules $myRuleScaleUp,$myRuleScaleDown `
  -Name "autoprofile"

# Apply hello autoscale rules
Add-AzureRmAutoscaleSetting `
  -Location $myLocation `
  -Name "autosetting" `
  -ResourceGroup $myResourceGroup `
  -TargetResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -AutoscaleProfiles $myScaleProfile
```


## <a name="next-steps"></a><span data-ttu-id="bd846-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bd846-163">Next steps</span></span>
<span data-ttu-id="bd846-164">W tym samouczku utworzony zestaw skali maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bd846-164">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="bd846-165">W tym samouczku omówiono:</span><span class="sxs-lookup"><span data-stu-id="bd846-165">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bd846-166">Użyj hello niestandardowe rozszerzenie skryptu toodefine tooscale witryny usług IIS</span><span class="sxs-lookup"><span data-stu-id="bd846-166">Use hello Custom Script Extension toodefine an IIS site tooscale</span></span>
> * <span data-ttu-id="bd846-167">Tworzenie modułu równoważenia obciążenia dla zestawu skalowania</span><span class="sxs-lookup"><span data-stu-id="bd846-167">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="bd846-168">Utwórz zestaw skali maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="bd846-168">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="bd846-169">Zwiększanie lub zmniejszanie hello liczbę wystąpień w zestawie skalowania</span><span class="sxs-lookup"><span data-stu-id="bd846-169">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="bd846-170">Tworzenie reguł skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="bd846-170">Create autoscale rules</span></span>

<span data-ttu-id="bd846-171">Więcej informacji na temat pojęć dla maszyn wirtualnych równoważenia obciążenia poprawić toohello dalej toolearn samouczka.</span><span class="sxs-lookup"><span data-stu-id="bd846-171">Advance toohello next tutorial toolearn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bd846-172">Równoważyć obciążenie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="bd846-172">Load balance virtual machines</span></span>](tutorial-load-balancer.md)
