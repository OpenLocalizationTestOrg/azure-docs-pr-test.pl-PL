---
title: zestaw skalowania maszyny wirtualnej platformy Azure aaaCreate | Dokumentacja firmy Microsoft
description: "Tworzenie i wdrażanie skali maszyny wirtualnej systemu Linux lub Windows Azure ustawiony za pomocą interfejsu wiersza polecenia Azure, programu PowerShell, szablonu lub Visual Studio."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 07/21/2017
ms.author: adegeo
ms.openlocfilehash: 73de25c1dd2424e64655b3accfea848926e72f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-a-virtual-machine-scale-set"></a>Tworzenie i wdrażanie zestaw skali maszyny wirtualnej
Zestawy skalowania maszyn wirtualnych ułatwiają możesz toodeploy i zarządzaj nimi wiele identycznych maszyn wirtualnych jako zestaw. Zestawy skalowania w przypadku aplikacji o dużej skali zapewnić warstwy obliczeniowej wysoce skalowalnemu i dostosowania i obsługują obrazów platformy systemu Windows, Linux platformy obrazów niestandardowych obrazów i rozszerzenia. Aby uzyskać więcej informacji na temat zestawów skalowania, zobacz [zestawy skalowania maszyny wirtualnej](virtual-machine-scale-sets-overview.md).

Ten samouczek pokazuje, jak toocreate zestawu skalowania maszyn wirtualnych **bez** przy użyciu hello portalu Azure. Aby uzyskać informacje o sposobie toouse hello portalu Azure, zobacz [jak toocreate, zestawu skalowania maszyn wirtualnych, z portalu Azure hello](virtual-machine-scale-sets-portal-create.md).

>[!NOTE]
>Aby uzyskać więcej informacji na temat zasobów usługi Azure Resource Manager, zobacz [usługi Azure Resource Manager, a wdrożenie klasyczne](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="sign-in-tooazure"></a>Zaloguj się tooAzure

Jeśli używasz interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub Azure PowerShell toocreate skali ustawiona, należy najpierw toosign w tooyour subskrypcji.

Aby uzyskać więcej informacji na temat sposobu tooinstall, konfigurowanie i zaloguj się tooAzure z wiersza polecenia platformy Azure lub programu PowerShell, zobacz [wprowadzenie Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) lub [wprowadzenie do poleceń cmdlet programu Azure PowerShell](/powershell/azure/overview).

```azurecli
az login
```

```powershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Należy najpierw toocreate grupę zasobów, której zestawu skalowania maszyn wirtualnych hello jest skojarzony z.

```azurecli
az group create --location westus2 --name MyResourceGroup1
```

```powershell
New-AzureRmResourceGroup -Location westus2 -Name MyResourceGroup1
```

## <a name="create-from-azure-cli"></a>Tworzenie z interfejsu wiersza polecenia platformy Azure

Z wiersza polecenia platformy Azure można utworzyć ustawianie przy minimalnym nakładzie pracy skali maszyny wirtualnej. W przypadku pominięcia wartości domyślne, są one udostępniane dla Ciebie. Na przykład jeśli nie określisz żadnych informacji sieci wirtualnej, sieci wirtualnej jest tworzony automatycznie. W przypadku pominięcia hello następujące części, ich są tworzone automatycznie: 
- Moduł równoważenia obciążenia
- Sieć wirtualna
- Publiczny adres IP

Podczas wybierania hello obraz maszyny wirtualnej, które mają toouse na zestaw skali maszyny wirtualnej hello, masz kilka opcji:

- URN  
Witaj identyfikator zasobu:  
**Win2012R2Datacenter**

- URN alias  
Witaj przyjaznej nazwy URN:  
**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**

- Identyfikator zasobu niestandardowego  
Ścieżka tooan Hello zasobów platformy Azure:  
**/Subscriptions/Subscription-GUID/resourceGroups/MyResourceGroup/Providers/Microsoft.COMPUTE/images/MyImage**

- Zasób sieci Web  
Ścieżka tooan Hello identyfikator URI protokołu HTTP:  
**http://contoso.blob.Core.Windows.NET/vhds/osdiskimage.VHD**

>[!TIP]
>Można uzyskać listę dostępnych obrazów z `az vm image list`.

Ustawianie skalowania maszyny wirtualnej toocreate, należy określić następujące hello:

- Grupa zasobów 
- Nazwa
- Obraz systemu operacyjnego
- Informacje dotyczące uwierzytelniania 
 
Witaj poniższy przykład tworzy zestaw skalowania podstawowej maszyny wirtualnej (ten krok może potrwać kilka minut).

```azurecli
az vmss create --resource-group MyResourceGroup1 --name MyScaleSet --image UbuntuLTS --authentication-type password --admin-username azureuser --admin-password P@ssw0rd!
```

Po zakończeniu działania polecenia hello trzeba będzie teraz Twojego zestaw utworzony skalowania maszyny wirtualnej. Adres IP hello tooget hello maszyny wirtualnej może być konieczne, dzięki czemu można łączyć tooit. Wiele różnych informacji o maszynie wirtualnej hello (łącznie z adresem IP hello) można uzyskać z hello następujące polecenia. 

```azurecli
az vmss list-instance-connection-info --resource-group MyResourceGroup1 --name MyScaleSet
```

## <a name="create-from-powershell"></a>Utwórz na podstawie programu PowerShell

PowerShell jest bardziej skomplikowany toouse niż wiersza polecenia platformy Azure. Interfejsu wiersza polecenia Azure zawiera ustawienia domyślne dla zasobów związanych z siecią (na przykład usługi równoważenia obciążenia, adresów IP i sieci wirtualne), natomiast nie obsługuje programu PowerShell. Odwołanie do obrazu przy użyciu programu PowerShell jest zbyt nieco bardziej skomplikowane. Obrazy można uzyskać z hello następującego polecenia cmdlet:

1. Get-AzureRMVMImagePublisher
2. Get-AzureRMVMImageOffer
3. Get-AzureRmVMImageSku

Hello pracy polecenia cmdlet mogą być przekazywane w potoku w sekwencji. Poniżej przedstawiono przykład sposobu tooget wszystkie obrazy dla hello **zachodnie stany USA 2** region z wydawcą o nazwie hello **microsoft** w nim.

```powershell
Get-AzureRMVMImagePublisher -Location WestUS2 | Where-Object PublisherName -Like *microsoft* | Get-AzureRMVMImageOffer | Get-AzureRmVMImageSku | Select-Object PublisherName, Offer, Skus
```

```
PublisherName              Offer                    Skus
-------------              -----                    ----
microsoft-ads              linux-data-science-vm    linuxdsvm
microsoft-ads              standard-data-science-vm standard-data-science-vm
MicrosoftAzureSiteRecovery Process-Server           Windows-2012-R2-Datacenter
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Enterprise
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Standard
MicrosoftBizTalkServer     BizTalk-Server           2016-Developer
MicrosoftBizTalkServer     BizTalk-Server           2016-Enterprise
...
```

Witaj przepływ pracy tworzenia zestawu skali maszyny wirtualnej jest następujący:

1. Utwórz obiekt konfiguracji, który przechowuje informacje o zestawie skali hello.
2. Odwołanie hello podstawowy obraz systemu operacyjnego.
3. Skonfiguruj ustawienia systemu operacyjnego hello: uwierzytelnianie, prefiks nazwy maszyny Wirtualnej i użytkownika/hasło.
4. Konfigurowanie sieci.
5. Utwórz zestaw skali hello.

W tym przykładzie tworzy zestaw na komputerze, na którym został zainstalowany program Windows Server 2016 podstawowe skalowania dwa wystąpienia.

```powershell
# Resource group name from above
$rg = "MyResourceGroup1"
$location = "WestUS2"

# Create a config object
$vmssConfig = New-AzureRmVmssConfig -Location $location -SkuCapacity 2 -SkuName Standard_A0  -UpgradePolicyMode Automatic

# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig -ImageReferencePublisher MicrosoftWindowsServer -ImageReferenceOffer WindowsServer -ImageReferenceSku 2016-Datacenter -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig -AdminUsername azureuser -AdminPassword P@ssw0rd! -ComputerNamePrefix myvmssvm

# Create hello virtual network resources

## Basics
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name "my-subnet" -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name "my-network" -ResourceGroupName $rg -Location $location -AddressPrefix 10.0.0.0/16 -Subnet $subnet

## Load balancer
$publicIP = New-AzureRmPublicIpAddress -Name "PublicIP" -ResourceGroupName $rg -Location $location -AllocationMethod Static -DomainNameLabel "myuniquedomain"
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontend" -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
$probe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
$inboundNATRule1= New-AzureRmLoadBalancerRuleConfig -Name "webserver" -FrontendIpConfiguration $frontendIP -Protocol Tcp -FrontendPort 80 -BackendPort 80 -IdleTimeoutInMinutes 15 -Probe $probe -BackendAddressPool $backendPool
$inboundNATPool1 = New-AzureRmLoadBalancerInboundNatPoolConfig -Name "RDP" -FrontendIpConfigurationId $frontendIP.Id -Protocol TCP -FrontendPortRangeStart 53380 -FrontendPortRangeEnd 53390 -BackendPort 3389

New-AzureRmLoadBalancer -ResourceGroupName $rg -Name "LB1" -Location $location -FrontendIpConfiguration $frontendIP -LoadBalancingRule $inboundNATRule1 -InboundNatPool $inboundNATPool1 -BackendAddressPool $backendPool -Probe $probe

## IP address config
$ipConfig = New-AzureRmVmssIpConfig -Name "my-ipaddress" -LoadBalancerBackendAddressPoolsId $backendPool.Id -SubnetId $vnet.Subnets[0].Id -LoadBalancerInboundNatPoolsId $inboundNATPool1.Id

# Attach hello virtual network toohello IP object
Add-AzureRmVmssNetworkInterfaceConfiguration -VirtualMachineScaleSet $vmssConfig -Name "network-config" -Primary $true -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss -ResourceGroupName $rg -Name "MyScaleSet1" -VirtualMachineScaleSet $vmssConfig
```

### <a name="using-a-custom-virtual-machine-image"></a>Przy użyciu obrazu niestandardowego maszyny wirtualnej
Jeśli tworzysz skali ustawiony na podstawie własny obraz niestandardowy, zamiast odwołujące się do obrazu maszyny wirtualnej z galerii hello hello _AzureRmVmssStorageProfile zestaw_ polecenie będzie wyglądać następująco:
```PowerShell
Set-AzureRmVmssStorageProfile -OsDiskCreateOption FromImage -ManagedDisk PremiumLRS -OsDiskCaching "None" -OsDiskOsType Linux -ImageReferenceId (Get-AzureRmImage -ImageName $VMImage -ResourceGroupName $rg).id
```

## <a name="create-from-a-template"></a>Tworzenie na podstawie szablonu

Można wdrożyć skali maszyny wirtualnej ustawić przy użyciu szablonu usługi Azure Resource Manager. Można utworzyć własny szablon lub użyj jednej z hello [repozytorium szablonu](https://azure.microsoft.com/resources/templates/?term=vmss). Szablony te można wdrożyć bezpośrednio tooyour subskrypcji platformy Azure.

>[!NOTE]
>toocreate własny szablon, Utwórz plik tekstowy w formacie JSON. Aby uzyskać ogólne informacje o tym, jak toocreate i dostosować szablon, zobacz [szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Dostępny jest przykładowy szablon [w serwisie GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set). Aby uzyskać więcej informacji na temat sposobu toocreate i użyj tego przykładowe, zobacz [zestaw wielkości co najmniej](.\virtual-machine-scale-sets-mvss-start.md).

## <a name="create-from-visual-studio"></a>Utwórz w programie Visual Studio

Z programem Visual Studio można Tworzenie projektu grupy zasobów platformy Azure i dodać szablon tooit zestawu skalowania maszyny wirtualnej. Można wybrać, czy ma tooimport go z usługi GitHub lub hello Galeria aplikacji sieci Web platformy Azure. Wdrożenie skryptu PowerShell zostanie również wygenerowany automatycznie. Aby uzyskać więcej informacji, zobacz [jak toocreate, zestawu skalowania maszyn wirtualnych, z programem Visual Studio](virtual-machine-scale-sets-vs-create.md).

## <a name="create-from-hello-azure-portal"></a>Utwórz na podstawie hello portalu Azure

Witaj portalu Azure oferują wygodny sposób tooquickly utworzyć zestaw skali. Aby uzyskać więcej informacji, zobacz [jak toocreate, zestawu skalowania maszyn wirtualnych, z portalu Azure hello](virtual-machine-scale-sets-portal-create.md).

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o [dysków z danymi](virtual-machine-scale-sets-attached-disks.md).

Dowiedz się, jak za[zarządzania aplikacjami](virtual-machine-scale-sets-deploy-app.md).
