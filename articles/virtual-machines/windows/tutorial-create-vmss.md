---
title: "Utwórz zestawy skalowania maszyny wirtualnej dla systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 6600d3b401495f6c291249935b16bcc36c9b8f4b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a><span data-ttu-id="727db-103">Tworzenie zestawu skalowania maszyny wirtualnej i wdrażanie wysokiej dostępności aplikacji w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="727db-103">Create a Virtual Machine Scale Set and deploy a highly available app on Windows</span></span>
<span data-ttu-id="727db-104">Zestaw skali maszyny wirtualnej umożliwia wdrażanie i zarządzanie nimi zestaw identyczne, automatyczne skalowanie maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="727db-104">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="727db-105">Można ręcznie skalować liczbę maszyn wirtualnych w zestawie skalowania lub definiowania reguł do skalowania automatycznego na podstawie użycia procesora CPU, pamięci żądanie lub ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="727db-105">You can scale the number of VMs in the scale set manually, or define rules to autoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="727db-106">W tym samouczku możesz wdrożyć skali maszyny wirtualnej w usłudze Azure.</span><span class="sxs-lookup"><span data-stu-id="727db-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="727db-107">Omawiane kwestie:</span><span class="sxs-lookup"><span data-stu-id="727db-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="727db-108">Umożliwia zdefiniowanie witryny usług IIS można skalować niestandardowe rozszerzenie skryptu</span><span class="sxs-lookup"><span data-stu-id="727db-108">Use the Custom Script Extension to define an IIS site to scale</span></span>
> * <span data-ttu-id="727db-109">Tworzenie modułu równoważenia obciążenia dla zestawu skalowania</span><span class="sxs-lookup"><span data-stu-id="727db-109">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="727db-110">Utwórz zestaw skali maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="727db-110">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="727db-111">Zwiększ lub Zmniejsz liczbę wystąpień w zestawie skalowania</span><span class="sxs-lookup"><span data-stu-id="727db-111">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="727db-112">Tworzenie reguł skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="727db-112">Create autoscale rules</span></span>

<span data-ttu-id="727db-113">Dla tego samouczka jest wymagany moduł Azure PowerShell w wersji 3.6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="727db-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="727db-114">Uruchom polecenie ` Get-Module -ListAvailable AzureRM`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="727db-114">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="727db-115">Jeśli potrzebujesz do uaktualnienia, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="727db-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="scale-set-overview"></a><span data-ttu-id="727db-116">Omówienie zestawu skali</span><span class="sxs-lookup"><span data-stu-id="727db-116">Scale Set overview</span></span>
<span data-ttu-id="727db-117">Zestawy skalowania używać podobne pojęcia poznanie w poprzednim w samouczku [tworzyć maszyny wirtualne o wysokiej dostępności](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="727db-117">Scale sets use similar concepts as you learned about in the previous tutorial to [Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="727db-118">Maszyny wirtualne w zestawie skalowania są dystrybuowane między domenami usterek i aktualizacji, podobnie jak maszyn wirtualnych w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="727db-118">VMs in a scale set are distributed across fault and update domains just like VMs in an availability set.</span></span>

<span data-ttu-id="727db-119">Maszyny wirtualne są tworzone zgodnie z potrzebami w zestawie skalowania.</span><span class="sxs-lookup"><span data-stu-id="727db-119">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="727db-120">Należy zdefiniować regułę automatycznego skalowania do kontrolowania sposobu i czasu maszyny wirtualne są dodawane lub usuwane z zestawu skalowania.</span><span class="sxs-lookup"><span data-stu-id="727db-120">You define autoscale rules to control how and when VMs are added or removed from the scale set.</span></span> <span data-ttu-id="727db-121">Te reguły może wyzwolić na podstawie metryk, takich jak obciążenie procesora CPU, pamięć lub ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="727db-121">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="727db-122">Skala ustawia obsługi maksymalnie 1000 maszyn wirtualnych, korzystając z obrazu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="727db-122">Scale sets support up to 1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="727db-123">W przypadku obciążeń z instalacją znaczących lub wymagania dotyczące dostosowywania maszyny Wirtualnej, warto [utworzyć niestandardowy obraz maszyny Wirtualnej](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="727db-123">For workloads with significant installation or VM customization requirements, you may wish to [Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="727db-124">Możesz utworzyć maksymalnie 100 maszyn wirtualnych w skali ustawić przy użyciu obrazu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="727db-124">You can create up to 100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-to-scale"></a><span data-ttu-id="727db-125">Utwórz aplikację do skalowania</span><span class="sxs-lookup"><span data-stu-id="727db-125">Create an app to scale</span></span>
<span data-ttu-id="727db-126">Przed utworzeniem zestaw skali, Utwórz grupę zasobów o [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="727db-126">Before you can create a scale set, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="727db-127">Poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupAutomate* w *EastUS* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="727db-127">The following example creates a resource group named *myResourceGroupAutomate* in the *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

<span data-ttu-id="727db-128">W starszych samouczka przedstawiono sposób [konfiguracji zautomatyzować maszyny Wirtualnej](tutorial-automate-vm-deployment.md) za pomocą niestandardowego rozszerzenia skryptu.</span><span class="sxs-lookup"><span data-stu-id="727db-128">In an earlier tutorial, you learned how to [Automate VM configuration](tutorial-automate-vm-deployment.md) using the Custom Script Extension.</span></span> <span data-ttu-id="727db-129">Tworzenie konfiguracji zestaw skali, a następnie zastosować niestandardowe rozszerzenie skryptu, aby zainstalować i skonfigurować usługi IIS:</span><span class="sxs-lookup"><span data-stu-id="727db-129">Create a scale set configuration then apply a Custom Script Extension to install and configure IIS:</span></span>

```powershell
# Create a config object
$vmssConfig = New-AzureRmVmssConfig `
    -Location EastUS `
    -SkuCapacity 2 `
    -SkuName Standard_DS2 `
    -UpgradePolicyMode Automatic

# Define the script for your Custom Script Extension to run
$publicSettings = @{
    "fileUris" = (,"https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate-iis.ps1");
    "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File automate-iis.ps1"
}

# Use Custom Script Extension to install IIS and configure basic website
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig `
    -Name "customScript" `
    -Publisher "Microsoft.Compute" `
    -Type "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -Setting $publicSettings
```

## <a name="create-scale-load-balancer"></a><span data-ttu-id="727db-130">Tworzenie usługi równoważenia obciążenia skali</span><span class="sxs-lookup"><span data-stu-id="727db-130">Create scale load balancer</span></span>
<span data-ttu-id="727db-131">Moduł równoważenia obciążenia Azure jest równoważenia obciążenia warstwy 4 (TCP, UDP), który zapewnia wysoką dostępność, przekazując przychodzący ruch między maszynami wirtualnymi w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="727db-131">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="727db-132">Badanie kondycji modułu równoważenia obciążenia monitoruje danego portu na każdej maszynie Wirtualnej i tylko dystrybuuje ruch do operacyjnej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="727db-132">A load balancer health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span> <span data-ttu-id="727db-133">Aby uzyskać więcej informacji, zobacz następny samouczek na [jak załadować saldo maszyn wirtualnych Windows](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="727db-133">For more information, see the next tutorial on [How to load balance Windows virtual machines](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="727db-134">Utwórz moduł równoważenia obciążenia, który ma publicznego adresu IP i rozpowszechnia ruchu w sieci web na porcie 80:</span><span class="sxs-lookup"><span data-stu-id="727db-134">Create a load balancer that has a public IP address and distributes web traffic on port 80:</span></span>

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

# Create the load balancer
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

# Create a load balancer rule to distribute traffic on port 80
Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80

# Update the load balancer configuration
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="create-a-scale-set"></a><span data-ttu-id="727db-135">Utwórz zestaw skali</span><span class="sxs-lookup"><span data-stu-id="727db-135">Create a scale set</span></span>
<span data-ttu-id="727db-136">Teraz Utwórz zestaw o skali maszyny wirtualnej [AzureRmVmss nowy](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="727db-136">Now create a virtual machine scale set with [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="727db-137">Poniższy przykład tworzy zestaw o nazwie skalowania *myScaleSet*:</span><span class="sxs-lookup"><span data-stu-id="727db-137">The following example creates a scale set named *myScaleSet*:</span></span>

```powershell
# Reference a virtual machine image from the gallery
Set-AzureRmVmssStorageProfile $vmssConfig `
  -ImageReferencePublisher MicrosoftWindowsServer `
  -ImageReferenceOffer WindowsServer `
  -ImageReferenceSku 2016-Datacenter `
  -ImageReferenceVersion latest

# Set up information for authenticating with the virtual machine
Set-AzureRmVmssOsProfile $vmssConfig `
  -AdminUsername azureuser `
  -AdminPassword P@ssword! `
  -ComputerNamePrefix myVM

# Create the virtual network resources
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

# Attach the virtual network to the config object
Add-AzureRmVmssNetworkInterfaceConfiguration `
  -VirtualMachineScaleSet $vmssConfig `
  -Name "network-config" `
  -Primary $true `
  -IPConfiguration $ipConfig

# Create the scale set with the config object (this step might take a few minutes)
New-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myScaleSet `
  -VirtualMachineScaleSet $vmssConfig
```

<span data-ttu-id="727db-138">Trwa kilka minut, aby utworzyć i skonfigurować zasoby zestaw skali i maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="727db-138">It takes a few minutes to create and configure all the scale set resources and VMs.</span></span>


## <a name="test-your-app"></a><span data-ttu-id="727db-139">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="727db-139">Test your app</span></span>
<span data-ttu-id="727db-140">Aby zapoznać się z witryny sieci Web usług IIS w akcji, uzyskania publicznego adresu IP z usługi równoważenia obciążenia z [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="727db-140">To see your IIS website in action, obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="727db-141">Poniższy przykład uzyskuje adres IP dla *myPublicIP* utworzona w ramach zestawu skali:</span><span class="sxs-lookup"><span data-stu-id="727db-141">The following example obtains the IP address for *myPublicIP* created as part of the scale set:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

<span data-ttu-id="727db-142">Wprowadź publicznego adresu IP w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="727db-142">Enter the public IP address in to a web browser.</span></span> <span data-ttu-id="727db-143">Aplikacja jest wyświetlana, łącznie z nazwą hosta maszyny Wirtualnej, ruch do dystrybucji modułu równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="727db-143">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to:</span></span>

![Uruchomionej witryny usług IIS](./media/tutorial-create-vmss/running-iis-site.png)

<span data-ttu-id="727db-145">Aby wyświetlić zestaw akcji skalowania, możesz można życie odświeżania przeglądarki sieci web, aby zobaczyć Dystrybuuj ruch na wszystkich maszynach wirtualnych z tą aplikacją usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="727db-145">To see the scale set in action, you can force-refresh your web browser to see the load balancer distribute traffic across all the VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="727db-146">Zadania zarządzania</span><span class="sxs-lookup"><span data-stu-id="727db-146">Management tasks</span></span>
<span data-ttu-id="727db-147">W całym cyklu życia zestawu skalowania konieczne może być Uruchom jedno lub więcej zadań zarządzania.</span><span class="sxs-lookup"><span data-stu-id="727db-147">Throughout the lifecycle of the scale set, you may need to run one or more management tasks.</span></span> <span data-ttu-id="727db-148">Ponadto można tworzenia skryptów automatyzujących różnych zadań cyklu życia.</span><span class="sxs-lookup"><span data-stu-id="727db-148">Additionally, you may want to create scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="727db-149">Program Azure PowerShell umożliwia szybkie do wykonywania tych zadań.</span><span class="sxs-lookup"><span data-stu-id="727db-149">Azure PowerShell provides a quick way to do those tasks.</span></span> <span data-ttu-id="727db-150">Poniżej przedstawiono kilka typowych zadań.</span><span class="sxs-lookup"><span data-stu-id="727db-150">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="727db-151">Maszyny wirtualne widoku w zestawie skalowania</span><span class="sxs-lookup"><span data-stu-id="727db-151">View VMs in a scale set</span></span>
<span data-ttu-id="727db-152">Aby wyświetlić listę uruchomionych w zestawie skalowania maszyn wirtualnych, użyj [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="727db-152">To view a list of VMs running in your scale set, use [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) as follows:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Loop through the instanaces in your scale set
for ($i=1; $i -le ($scaleset.Sku.Capacity - 1); $i++) {
    Get-AzureRmVmssVM -ResourceGroupName myResourceGroupScaleSet `
      -VMScaleSetName myScaleSet `
      -InstanceId $i
}
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="727db-153">Zwiększanie lub zmniejszanie wystąpień maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="727db-153">Increase or decrease VM instances</span></span>
<span data-ttu-id="727db-154">Aby wyświetlić liczbę wystąpień aktualnie zainstalowana w zestawie skalowania, użyj [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) i wykonywać zapytania na *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="727db-154">To see the number of instances you currently have in a scale set, use [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) and query on *sku.capacity*:</span></span>

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

<span data-ttu-id="727db-155">Możesz ręcznie zwiększyć lub zmniejszyć liczbę maszyn wirtualnych w skali ustawiony za pomocą [AzureRmVmss aktualizacji](/powershell/module/azurerm.compute/update-azurermvmss).</span><span class="sxs-lookup"><span data-stu-id="727db-155">You can then manually increase or decrease the number of virtual machines in the scale set with [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss).</span></span> <span data-ttu-id="727db-156">Poniższy przykład ustawia liczbę maszyn wirtualnych w skali, z ustawioną *5*:</span><span class="sxs-lookup"><span data-stu-id="727db-156">The following example sets the number of VMs in your scale set to *5*:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Set and update the capacity of your scale set
$scaleset.sku.capacity = 5
Update-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -Name myScaleSet `
    -VirtualMachineScaleSet $scaleset
```

<span data-ttu-id="727db-157">Jeśli ustawiona przyjmuje kilka minut, aby zaktualizować określoną liczbę wystąpień w skali sieci.</span><span class="sxs-lookup"><span data-stu-id="727db-157">If takes a few minutes to update the specified number of instances in your scale set.</span></span>


### <a name="configure-autoscale-rules"></a><span data-ttu-id="727db-158">Konfigurowanie reguł automatycznego skalowania</span><span class="sxs-lookup"><span data-stu-id="727db-158">Configure autoscale rules</span></span>
<span data-ttu-id="727db-159">Zamiast ręcznie skalowanie liczby wystąpień w skali sieci, należy zdefiniować regułę automatycznego skalowania.</span><span class="sxs-lookup"><span data-stu-id="727db-159">Rather than manually scaling the number of instances in your scale set, you define autoscale rules.</span></span> <span data-ttu-id="727db-160">Te reguły monitorować wystąpienia w zestawie skali i Odpowiedz, odpowiednio na podstawie metryk i progów, które należy zdefiniować.</span><span class="sxs-lookup"><span data-stu-id="727db-160">These rules monitor the instances in your scale set and respond accordingly based on metrics and thresholds you define.</span></span> <span data-ttu-id="727db-161">Limit liczby wystąpień programu przez jedną skaluje poniższy przykład, gdy średni obciążenie procesora CPU jest większy niż 60% w okresie 5 minut.</span><span class="sxs-lookup"><span data-stu-id="727db-161">The following example scales out the number of instances by one when the average CPU load is greater than 60% over a 5 minute period.</span></span> <span data-ttu-id="727db-162">Jeśli w okresie 5 minut średnie obciążenie procesora CPU spadnie poniżej 30%, wystąpienia są skalowane w przez jedno wystąpienie:</span><span class="sxs-lookup"><span data-stu-id="727db-162">If the average CPU load then drops below 30% over a 5 minute period, the instances are scaled in by one instance:</span></span>

```powershell
# Define your scale set information
$mySubscriptionId = (Get-AzureRmSubscription).Id
$myResourceGroup = "myResourceGroupScaleSet"
$myScaleSet = "myScaleSet"
$myLocation = "East US"

# Create a scale up rule to increase the number instances after 60% average CPU usage exceeded for a 5 minute period
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

# Create a scale down rule to decrease the number of instances after 30% average CPU usage over a 5 minute period
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

# Apply the autoscale rules
Add-AzureRmAutoscaleSetting `
  -Location $myLocation `
  -Name "autosetting" `
  -ResourceGroup $myResourceGroup `
  -TargetResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -AutoscaleProfiles $myScaleProfile
```


## <a name="next-steps"></a><span data-ttu-id="727db-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="727db-163">Next steps</span></span>
<span data-ttu-id="727db-164">W tym samouczku utworzony zestaw skali maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="727db-164">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="727db-165">Możesz przedstawiono sposób do:</span><span class="sxs-lookup"><span data-stu-id="727db-165">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="727db-166">Umożliwia zdefiniowanie witryny usług IIS można skalować niestandardowe rozszerzenie skryptu</span><span class="sxs-lookup"><span data-stu-id="727db-166">Use the Custom Script Extension to define an IIS site to scale</span></span>
> * <span data-ttu-id="727db-167">Tworzenie modułu równoważenia obciążenia dla zestawu skalowania</span><span class="sxs-lookup"><span data-stu-id="727db-167">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="727db-168">Utwórz zestaw skali maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="727db-168">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="727db-169">Zwiększ lub Zmniejsz liczbę wystąpień w zestawie skalowania</span><span class="sxs-lookup"><span data-stu-id="727db-169">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="727db-170">Tworzenie reguł skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="727db-170">Create autoscale rules</span></span>

<span data-ttu-id="727db-171">Przejdź do następnego samouczek, aby dowiedzieć się więcej na temat pojęć dla maszyn wirtualnych równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="727db-171">Advance to the next tutorial to learn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="727db-172">Równoważyć obciążenie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="727db-172">Load balance virtual machines</span></span>](tutorial-load-balancer.md)
