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
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a>Tworzenie zestawu skalowania maszyny wirtualnej i wdrażanie wysokiej dostępności aplikacji w systemie Windows
Zestaw skali maszyny wirtualnej umożliwia toodeploy i zarządzać zestawem identyczne, automatyczne skalowanie maszyn wirtualnych. Można ręcznie skalować hello liczbę maszyn wirtualnych w zestawie skalowania hello lub zdefiniuj tooautoscale reguły na podstawie użycia procesora CPU, pamięci żądanie lub ruchu sieciowego. W tym samouczku możesz wdrożyć skali maszyny wirtualnej w usłudze Azure. Omawiane kwestie:

> [!div class="checklist"]
> * Użyj hello niestandardowe rozszerzenie skryptu toodefine tooscale witryny usług IIS
> * Tworzenie modułu równoważenia obciążenia dla zestawu skalowania
> * Utwórz zestaw skali maszyny wirtualnej
> * Zwiększanie lub zmniejszanie hello liczbę wystąpień w zestawie skalowania
> * Tworzenie reguł skalowania automatycznego

Ten samouczek wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej. Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji. Jeśli potrzebujesz tooupgrade, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).


## <a name="scale-set-overview"></a>Omówienie zestawu skali
Zestawy skalowania używać podobne pojęcia poznanie w samouczku poprzedniej hello zbyt[tworzyć maszyny wirtualne o wysokiej dostępności](tutorial-availability-sets.md). Maszyny wirtualne w zestawie skalowania są dystrybuowane między domenami usterek i aktualizacji, podobnie jak maszyn wirtualnych w zestawie dostępności.

Maszyny wirtualne są tworzone zgodnie z potrzebami w zestawie skalowania. Zdefiniuj toocontrol reguł skalowania automatycznego, kiedy maszyny wirtualne są dodawane lub usuwane z hello zestaw skali. Te reguły może wyzwolić na podstawie metryk, takich jak obciążenie procesora CPU, pamięć lub ruchu sieciowego.

Obsługa się too1, 000 maszyn wirtualnych, gdy używasz obrazu platformy Azure zestawach skali. W przypadku obciążeń z instalacją znaczących lub wymagania dotyczące dostosowywania maszyny Wirtualnej, możesz za[utworzyć niestandardowy obraz maszyny Wirtualnej](tutorial-custom-images.md). Możesz utworzyć zapasowych maszyn wirtualnych too100 w skali ustawić przy użyciu obrazu niestandardowego.


## <a name="create-an-app-tooscale"></a>Utwórz tooscale aplikacji
Przed utworzeniem zestaw skali, Utwórz grupę zasobów o [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupAutomate* w hello *EastUS* lokalizacji:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

W starszych samouczka przedstawiono sposób zbyt[konfiguracji zautomatyzować maszyny Wirtualnej](tutorial-automate-vm-deployment.md) przy użyciu hello niestandardowe rozszerzenie skryptu. Utwórz konfigurację zestaw skali, a następnie Zastosuj tooinstall niestandardowe rozszerzenie skryptu i skonfigurować usługi IIS:

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

## <a name="create-scale-load-balancer"></a>Tworzenie usługi równoważenia obciążenia skali
Moduł równoważenia obciążenia Azure jest równoważenia obciążenia warstwy 4 (TCP, UDP), który zapewnia wysoką dostępność, przekazując przychodzący ruch między maszynami wirtualnymi w dobrej kondycji. Kondycji sondę modułu równoważenia obciążenia monitoruje danego portu na każdej maszynie Wirtualnej, a tylko dystrybuuje ruch tooan operacyjne maszyny Wirtualnej. Aby uzyskać więcej informacji, zobacz następny samouczek hello na [jak tooload złoty środek między maszynami wirtualnymi systemu Windows](tutorial-load-balancer.md).

Utwórz moduł równoważenia obciążenia, który ma publicznego adresu IP i rozpowszechnia ruchu w sieci web na porcie 80:

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

## <a name="create-a-scale-set"></a>Utwórz zestaw skali
Teraz Utwórz zestaw o skali maszyny wirtualnej [AzureRmVmss nowy](/powershell/module/azurerm.compute/new-azurermvm). Witaj poniższy przykład tworzy zestaw o nazwie skalowania *myScaleSet*:

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

Go zajmuje kilka minut toocreate i skonfiguruje wszystkie zasoby zestaw skalowania hello maszyn wirtualnych.


## <a name="test-your-app"></a>Testowanie aplikacji
toosee witryny sieci Web programu IIS w akcji, Uzyskaj hello publicznego adresu IP z usługi równoważenia obciążenia z [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Witaj poniższy przykład uzyskuje hello adres IP dla *myPublicIP* utworzone jako część zestawu skalowania hello:

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

Wprowadź hello publicznego adresu IP w przeglądarce sieci web tooa. Aplikacja Hello jest wyświetlana, łącznie z nazwą hosta hello hello hello tej maszyny Wirtualnej obciążenia ruchu równoważenia dystrybuowane do:

![Uruchomionej witryny usług IIS](./media/tutorial-create-vmss/running-iis-site.png)

zestaw w akcji skalowania hello toosee, możesz można życie odświeżania obciążenia hello toosee przeglądarki sieci web równoważenia rozpowszechniają wszystkich aplikacji uruchomionych maszyn wirtualnych hello ruchu.


## <a name="management-tasks"></a>Zadania zarządzania
W całym cyklu życia hello zestawu skali hello, może być konieczne toorun jednego lub więcej zadań zarządzania. Ponadto można toocreate skrypty, które automatyzacji różnych zadań cyklu życia. Program Azure PowerShell udostępnia toodo szybko tych zadań. Poniżej przedstawiono kilka typowych zadań.

### <a name="view-vms-in-a-scale-set"></a>Maszyny wirtualne widoku w zestawie skalowania
Ustaw listę maszyn wirtualnych uruchomionych w skali sieci tooview, użyj [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) w następujący sposób:

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


### <a name="increase-or-decrease-vm-instances"></a>Zwiększanie lub zmniejszanie wystąpień maszyn wirtualnych
toosee hello liczbę wystąpień obecnie w skali ustawiono, użyj [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) i wykonywać zapytania na *sku.capacity*:

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

Możesz ręcznie zwiększyć lub zmniejszyć liczbę hello maszyn wirtualnych w skali hello ustawiony za pomocą [AzureRmVmss aktualizacji](/powershell/module/azurerm.compute/update-azurermvmss). Witaj poniższy przykład przedstawia hello liczbę maszyn wirtualnych w sieci za zestaw skalowania*5*:

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

Jeśli zajmuje kilka minut tooupdate hello określona liczba wystąpień w zestawie skali.


### <a name="configure-autoscale-rules"></a>Konfigurowanie reguł automatycznego skalowania
Zamiast ręcznie skalowania hello liczbę wystąpień w skali sieci, należy zdefiniować regułę automatycznego skalowania. Te reguły monitorować hello wystąpień w skali sieci ustawić i odpowiedzi, w związku z tym na podstawie metryk i progów, które należy zdefiniować. Poniższy przykład Hello skaluje hello liczbę wystąpień przez jedną gdy obciążenie procesora CPU średni hello jest większy niż 60% w okresie 5 minut. Jeśli w okresie 5 minut obciążenia procesora CPU średnia hello spadnie poniżej 30%, wystąpień hello są skalowane w przez jedno wystąpienie:

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


## <a name="next-steps"></a>Następne kroki
W tym samouczku utworzony zestaw skali maszyny wirtualnej. W tym samouczku omówiono:

> [!div class="checklist"]
> * Użyj hello niestandardowe rozszerzenie skryptu toodefine tooscale witryny usług IIS
> * Tworzenie modułu równoważenia obciążenia dla zestawu skalowania
> * Utwórz zestaw skali maszyny wirtualnej
> * Zwiększanie lub zmniejszanie hello liczbę wystąpień w zestawie skalowania
> * Tworzenie reguł skalowania automatycznego

Więcej informacji na temat pojęć dla maszyn wirtualnych równoważenia obciążenia poprawić toohello dalej toolearn samouczka.

> [!div class="nextstepaction"]
> [Równoważyć obciążenie maszyn wirtualnych](tutorial-load-balancer.md)
