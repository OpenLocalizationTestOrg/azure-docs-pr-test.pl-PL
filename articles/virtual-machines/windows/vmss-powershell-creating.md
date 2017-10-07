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
# <a name="creating-virtual-machine-scale-sets-using-powershell-cmdlets"></a>Tworzenie zestawów skali maszyny wirtualnej za pomocą poleceń cmdlet programu PowerShell
W tym artykule przedstawiono przykład sposobu toocreate zestawu skalowania maszyn wirtualnych (VMSS). Tworzy zestaw skalowania trzy węzły z skojarzone sieci i magazynu.

## <a name="first-steps"></a>Pierwsze kroki
Upewnij się, masz hello zainstalowane najnowsze modułu Azure PowerShell, toomake upewnić się, że polecenia cmdlet środowiska PowerShell hello potrzeby toomaintain i utworzyć zestawy skalowania.
Przejdź do narzędzia wiersza polecenia toohello [tutaj](http://aka.ms/webpi-azps) dla hello najnowszych dostępnych modułów Azure.

polecenia cmdlet związane z toofind VMSS, użyj ciągu wyszukiwania hello \*VMSS\*. Na przykład _gcm *vmss*_

## <a name="creating-a-vmss"></a>Tworzenie VMSS
#### <a name="create-resource-group"></a>Tworzenie grupy zasobów
```
$loc = 'westus';
$rgname = 'mynewrgwu';
  New-AzureRmResourceGroup -Name $rgname -Location $loc -Force;
```

### <a name="create-networking-vnet--subnet"></a>Tworzenie sieci (Wirtualnej / podsieci)
#### <a name="subnet-specification"></a>Specyfikacja podsieci
```
$subnetName = 'websubnet'
  $subnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix "10.0.0.0/24";
```

#### <a name="vnet-specification"></a>Specyfikacja sieci Wirtualnej
```
$vnet = New-AzureRmVirtualNetwork -Force -Name ('vnet' + $rgname) -ResourceGroupName $rgname -Location $loc -AddressPrefix "10.0.0.0/16" -Subnet $subnet;
$vnet = Get-AzureRmVirtualNetwork -Name ('vnet' + $rgname) -ResourceGroupName $rgname;

# In this case assume hello new subnet is hello only one
$subnetId = $vnet.Subnets[0].Id;
```

#### <a name="create-public-ip-resource-tooallow-external-access"></a>Tworzenie publicznego adresu IP zasobu tooAllow dostępu zewnętrznego
Są to toohello powiązanej usługi równoważenia obciążenia.

```
$pubip = New-AzureRmPublicIpAddress -Force -Name ('pubip' + $rgname) -ResourceGroupName $rgname -Location $loc -AllocationMethod Dynamic -DomainNameLabel ('pubip' + $rgname);
$pubip = Get-AzureRmPublicIpAddress -Name ('pubip' + $rgname) -ResourceGroupName $rgname;
```

#### <a name="create-load-balancer"></a>Tworzenie usługi równoważenia obciążenia
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

#### <a name="configure-load-balancer"></a>Konfigurowanie usługi równoważenia obciążenia
Tworzenie konfiguracji puli adresów zaplecza, to będzie udostępniany przez karty sieciowe hello hello maszyn wirtualnych w zestawie skalowania hello.

```
$backendAddressPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name $backendAddressPoolName
```

Ustawiony Port sondy z równoważeniem obciążenia, Zmień ustawienia hello odpowiedni dla twojej aplikacji.

```
$probe = New-AzureRmLoadBalancerProbeConfig -Name $probeName -RequestPath healthcheck.aspx -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
```

Tworzenie puli NAT dla ruchu przychodzącego bezpośrednie połączenie między kierowanymi (zrównoważonym obciążeniu) toohello maszyn wirtualnych w skali hello ustawionych wcześniej za pośrednictwem hello moduł równoważenia obciążenia. To jest toodemonstrate za pomocą protokołu RDP i nie mogą być wymagane w aplikacji.

```
$frontendpoolrangestart = 3360
$frontendpoolrangeend = 3370
$backendvmport = 3389
$inboundNatPool = New-AzureRmLoadBalancerInboundNatPoolConfig -Name $inboundNatPoolName -FrontendIPConfigurationId `
$frontend.Id -Protocol Tcp -FrontendPortRangeStart $frontendpoolrangestart -FrontendPortRangeEnd $frontendpoolrangeend -BackendPort $backendvmport;
```

Utwórz hello załadować zrównoważonym reguły w przykładzie przedstawiono załadować równoważenia port 80 żądań, przy użyciu ustawień hello z poprzednich kroków.

```
$protocol = 'Tcp'
$feLBPort = 80
$beLBPort = 80

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name $lbruleName `
-FrontendIPConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -Protocol $protocol -FrontendPort $feLBPort -BackendPort $beLBPort `
-IdleTimeoutInMinutes 15 -EnableFloatingIP -LoadDistribution SourceIP -Verbose;
```

Utwórz moduł równoważenia obciążenia w konfiguracji.

```
$actualLb = New-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname -Location $loc `
-FrontendIpConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -LoadBalancingRule $lbrule -InboundNatPool $inboundNatPool -Verbose;
```

Sprawdź ustawienia LB, sprawdź obciążenia configs zrównoważonym portów, należy zwrócić uwagę, nie będzie mógł przeglądać reguły NAT ruchu przychodzącego do hello maszyn wirtualnych w zestawie skalowania hello są tworzone.

```
$expectedLb = Get-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname
```

##### <a name="configure-and-create-hello-scale-set"></a>Skonfigurowania i Utwórz hello skali
Uwaga: w tym przykładzie infrastruktury pokazano sposób dystrybucji tooset w górę i skalowania ruchu w sieci web przez zestaw skali hello, ale hello obrazów maszyn wirtualnych określone w tym miejscu nie mają żadnych zainstalowanych usług sieci web.

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

Powiąż tooLoad karta sieciowa usługi równoważenia i podsieci

```
$ipCfg = New-AzureRmVmssIPConfig -Name 'nic' `
-LoadBalancerInboundNatPoolsId $actualLb.InboundNatPools[0].Id `
-LoadBalancerBackendAddressPoolsId $actualLb.BackendAddressPools[0].Id `
-SubnetId $subnetId;
```

Utwórz skali set Config

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

Konfiguracja zestawu skali kompilacji

```
New-AzureRmVmss -ResourceGroupName $rgname -Name $vmssName -VirtualMachineScaleSet $vmss -Verbose;
```

Zestaw skali hello został utworzony. Można przetestować połączenia toohello poszczególnych maszyn wirtualnych za pomocą protokołu RDP w tym przykładzie:

```
VM0 : pubipmynewrgwu.westus.cloudapp.azure.com:3360
VM1 : pubipmynewrgwu.westus.cloudapp.azure.com:3361
VM2 : pubipmynewrgwu.westus.cloudapp.azure.com:3362
```
