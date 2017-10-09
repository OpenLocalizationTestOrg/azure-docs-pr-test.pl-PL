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
# <a name="how-tooload-balance-windows-virtual-machines-in-azure-toocreate-a-highly-available-application"></a>Jak tooload saldo maszyny wirtualne systemu Windows Azure toocreate wysokiej dostępności aplikacji
Równoważenie obciążenia sieciowego zapewnia wyższy poziom dostępności dzięki rozproszeniu przychodzące żądania między wieloma maszynami wirtualnymi. Z tego samouczka dowiesz się o hello różnych składników usługi równoważenia obciążenia Azure hello dystrybucji ruchu, które zapewniają wysoką dostępność. Omawiane kwestie:

> [!div class="checklist"]
> * Tworzenie usługi równoważenia obciążenia Azure
> * Utwórz kondycji sondę modułu równoważenia obciążenia
> * Tworzenie reguły ruchu usługi równoważenia obciążenia
> * Użyj hello niestandardowe rozszerzenie skryptu toocreate podstawowej witryny usług IIS
> * Tworzenie maszyn wirtualnych i Dołącz tooa modułu równoważenia obciążenia
> * Wyświetl modułu równoważenia obciążenia w akcji
> * Dodawanie i usuwanie maszyny wirtualne z modułem równoważenia obciążenia

Ten samouczek wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej. Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji. Jeśli potrzebujesz tooupgrade, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).


## <a name="azure-load-balancer-overview"></a>Omówienie usługi równoważenia obciążenia Azure
Moduł równoważenia obciążenia Azure jest równoważenia obciążenia warstwy 4 (TCP, UDP), który zapewnia wysoką dostępność, przekazując przychodzący ruch między maszynami wirtualnymi w dobrej kondycji. Kondycji sondę modułu równoważenia obciążenia monitoruje danego portu na każdej maszynie Wirtualnej, a tylko dystrybuuje ruch tooan operacyjne maszyny Wirtualnej.

Należy zdefiniować frontonu konfiguracji adresu IP, który zawiera co najmniej jeden publiczny adres IP. Ta konfiguracja frontonu IP umożliwia toobe, a aplikacje usługi równoważenia obciążenia dostępny za pośrednictwem hello Internet. 

Maszyny wirtualne połączenie usługi równoważenia obciążenia tooa przy użyciu ich karty interfejsu sieci wirtualnej (NIC). toodistribute toohello ruch maszyn wirtualnych, puli adresów zaplecza zawiera adresy IP hello hello wirtualnych (NIC) toohello podłączonej usługi równoważenia obciążenia.

toocontrol hello przepływu ruchu, należy zdefiniować reguły modułu równoważenia obciążenia dla określonych portów i protokołów, które mapują tooyour maszyn wirtualnych.


## <a name="create-azure-load-balancer"></a>Tworzenie usługi równoważenia obciążenia Azure
W tej sekcji Szczegóły, jak można tworzyć i konfigurować poszczególnych składników usługi równoważenia obciążenia hello. Przed utworzeniem przez moduł równoważenia obciążenia, Utwórz nową grupę zasobów o [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupLoadBalancer* w hello *EastUS* lokalizacji:

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a>Tworzenie publicznego adresu IP
tooaccess aplikacji na hello Internet, należy publicznego adresu IP dla modułu równoważenia obciążenia hello. Utwórz publiczny adres IP z [AzureRmPublicIpAddress nowy](/powershell/module/azurerm.network/new-azurermpublicipaddress). Witaj poniższy przykład tworzy publiczny adres IP o nazwie *myPublicIP* w hello *myResourceGroupLoadBalancer* grupy zasobów:

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a>Tworzenie modułu równoważenia obciążenia
Utwórz na adres IP frontonu [AzureRmLoadBalancerFrontendIpConfig nowy](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig). Witaj poniższy przykład tworzy adresu IP serwera sieci Web o nazwie *myFrontEndPool*: 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

Utwórz pulę adresów zaplecza z [AzureRmLoadBalancerBackendAddressPoolConfig nowy](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig). Witaj poniższy przykład tworzy puli adresów zaplecza, o nazwie *myBackEndPool*:

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

Teraz utworzymy hello modułu równoważenia obciążenia z [AzureRmLoadBalancer nowy](/powershell/module/azurerm.network/new-azurermloadbalancer). Witaj poniższy przykład tworzy moduł równoważenia obciążenia o nazwie *myLoadBalancer* przy użyciu hello *myPublicIP* adres:

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a>Utworzyć sondy kondycji
tooallow hello stanu usługi równoważenia obciążenia toomonitor hello aplikacji, możesz użyć sondy kondycji. sondy kondycji Hello dynamicznie dodaje lub usuwa maszyn wirtualnych z obrotu usługi równoważenia obciążenia hello oparte na ich kontroli toohealth odpowiedzi. Domyślnie maszyny Wirtualnej zostanie usunięte z dystrybucji modułu równoważenia obciążenia powitania po dwóch kolejnych błędów na 15 sekund. Można utworzyć sondy kondycji, na podstawie protokołu lub stronę wyboru kondycji określonych aplikacji. 

Witaj poniższy przykład tworzy badanie TCP. Można również utworzyć niestandardowe sond HTTP więcej kontroli kondycji szczegółowe. Podczas korzystania z niestandardowego badanie HTTP, należy utworzyć hello strona sprawdzania kondycji, takich jak *healthcheck.aspx*. Sonda Hello musi zwracać **HTTP 200 OK** odpowiedzi dla hosta usługi równoważenia obciążenia hello hello tookeep rotacji.

Użyj toocreate sondy kondycji TCP [AzureRmLoadBalancerProbeConfig Dodaj](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig). Witaj poniższy przykład tworzy badanie kondycji o nazwie *myHealthProbe* który monitoruje każdej maszyny Wirtualnej:

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

Zaktualizuj hello modułu równoważenia obciążenia z [AzureRmLoadBalancer zestaw](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a>Tworzenie reguły modułu równoważenia obciążenia
Reguły modułu równoważenia obciążenia jest używany toodefine sposób ruch jest rozproszonej toohello maszyn wirtualnych. Należy zdefiniować hello frontonu konfigurację adresu IP dla ruchu przychodzącego hello i hello zaplecza IP puli tooreceive hello ruchu, wraz z hello wymagane źródłowy i port docelowy. toomake się, że tylko dobrej kondycji maszyn wirtualnych odbieranie ruchu, możesz również definiować toouse sondy kondycji hello.

Tworzenie reguły modułu równoważenia obciążenia z [AzureRmLoadBalancerRuleConfig Dodaj](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig). Witaj poniższy przykład tworzy regułę równoważenia obciążenia o nazwie *myLoadBalancerRule* i równoważy ruch na porcie *80*:

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

Zaktualizuj hello modułu równoważenia obciążenia z [AzureRmLoadBalancer zestaw](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a>Konfigurowanie sieci wirtualnej
Przed wdrożeniem niektórych maszyn wirtualnych i przetestować z usługi równoważenia, Utwórz hello obsługi zasobów sieci wirtualnej. Aby uzyskać więcej informacji o sieciach wirtualnych, zobacz hello [Zarządzanie sieciami wirtualnymi Azure](tutorial-virtual-network.md) samouczka.

### <a name="create-network-resources"></a>Utwórz zasoby sieciowe
Tworzenie sieci wirtualnej z [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). Witaj poniższy przykład tworzy sieć wirtualną o nazwie *myVnet* z *mySubnet*:

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

Tworzenie reguły grupy zabezpieczeń sieci z [AzureRmNetworkSecurityRuleConfig nowy](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), należy utworzyć grupę zabezpieczeń sieci z [AzureRmNetworkSecurityGroup nowy](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup). Dodaj podsieć toohello grupy zabezpieczeń sieci hello z [AzureRmVirtualNetworkSubnetConfig zestaw](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) , a następnie zaktualizować sieci wirtualnej hello o [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork). 

Witaj poniższy przykład tworzy regułę grupy zabezpieczeń sieci o nazwie *myNetworkSecurityGroup* i stosuje je zbyt*mySubnet*:

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

Wirtualne karty sieciowe są tworzone za pomocą [AzureRmNetworkInterface nowy](/powershell/module/azurerm.network/new-azurermnetworkinterface). Witaj poniższy przykład tworzy trzy wirtualne karty sieciowe. (Jedną wirtualną kartę Sieciową dla każdej maszyny Wirtualnej można utworzyć dla aplikacji w hello następujące kroki). Można tworzyć dodatkowe wirtualne karty sieciowe i maszyn wirtualnych w dowolnym momencie i dodać je toohello usługi równoważenia obciążenia:

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

## <a name="create-virtual-machines"></a>Tworzenie maszyn wirtualnych
tooimprove hello wysoką dostępność aplikacji, umieść maszyn wirtualnych w zestawie dostępności.

Utwórz zestaw o dostępności [AzureRmAvailabilitySet nowy](/powershell/module/azurerm.compute/new-azurermavailabilityset). Witaj poniższy przykład tworzy zbiór nazwanego dostępności *myAvailabilitySet*:

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

Ustaw nazwę użytkownika i hasło administratora dla maszyn wirtualnych hello z [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Teraz można tworzyć maszyn wirtualnych hello o [AzureRmVM nowy](/powershell/module/azurerm.compute/new-azurermvm). Witaj poniższy przykład tworzy trzech maszyn wirtualnych:

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

Go zajmuje kilka minut toocreate i skonfiguruj wszystkie trzy maszyny wirtualne.

### <a name="install-iis-with-custom-script-extension"></a>Instalowanie usług IIS przy użyciu niestandardowego rozszerzenia skryptu
W poprzednich samouczek dotyczący [jak toocustomize maszyny wirtualnej systemu Windows](tutorial-automate-vm-deployment.md), wiesz, jak tooautomate dostosowywania maszyny Wirtualnej z hello niestandardowe rozszerzenie skryptu systemu Windows. Można użyć hello sam podejścia tooinstall i skonfigurowanie usług IIS na maszyny wirtualne.

Użyj [AzureRmVMExtension zestaw](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello niestandardowe rozszerzenie skryptu. Witaj uruchamia rozszerzenia `powershell Add-WindowsFeature Web-Server` tooinstall hello serwer sieci Web usług IIS, a następnie aktualizacje hello *Default.htm* strony tooshow hello nazwy hosta hello maszyny Wirtualnej:

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

## <a name="test-load-balancer"></a>Test usługi równoważenia obciążenia
Uzyskaj hello publicznego adresu IP z usługi równoważenia obciążenia z [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Witaj poniższy przykład uzyskuje hello adres IP dla *myPublicIP* utworzony wcześniej:

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

W przeglądarce sieci web tooa można następnie wprowadzić hello publicznego adresu IP. Hello witryny sieci Web jest wyświetlany, łącznie z nazwą hosta hello hello maszyny Wirtualnej tego modułu równoważenia obciążenia hello rozproszonych tooas ruchu w hello poniższy przykład:

![Witryna sieci Web IIS uruchomiona](./media/tutorial-load-balancer/running-iis-website.png)

Moduł równoważenia obciążenia hello toosee Dystrybuuj ruch we wszystkich trzech maszyn wirtualnych z tą aplikacją, użytkownik może życie odświeżania przeglądarki sieci web.


## <a name="add-and-remove-vms"></a>Dodawanie i usuwanie maszyny wirtualne
Może być konieczne tooperform konserwacji na powitania maszyn wirtualnych z tą aplikacją, takich jak instalowanie aktualizacji systemu operacyjnego. toodeal z aplikacją tooyour zwiększenie obciążenia, może być konieczne tooadd kolejnych maszyn wirtualnych. W tej sekcji opisano sposób tooremove lub dodać maszyny Wirtualnej z hello modułu równoważenia obciążenia.

### <a name="remove-a-vm-from-hello-load-balancer"></a>Usuń Maszynę wirtualną z hello modułu równoważenia obciążenia
Pobierz hello karty interfejsu sieciowego z [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), następnie zestaw hello *Loadbalancerbackendaddresspool* właściwość hello wirtualnej karty Sieciowej, za*$null*. Na koniec zaktualizuj hello wirtualnych kart sieciowych.:

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

Moduł równoważenia obciążenia hello toosee rozpowszechniają ruchu hello dwóch pozostałych maszyn wirtualnych z tą aplikacją możesz można życie odświeżania przeglądarki sieci web. Teraz można przeprowadzać konserwacji na powitania maszynę Wirtualną, takie jak instalowanie aktualizacji systemu operacyjnego lub wykonywania ponownego uruchomienia maszyny Wirtualnej.

### <a name="add-a-vm-toohello-load-balancer"></a>Dodaj usługi równoważenia obciążenia toohello maszyny Wirtualnej
Po konserwacja maszyny Wirtualnej lub tooexpand pojemności, należy ustawić hello *Loadbalancerbackendaddresspool* właściwości hello wirtualnej karty Sieciowej toohello *BackendAddressPool* z [ Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):

Pobierz hello usługi równoważenia obciążenia:

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a>Następne kroki

W tym samouczku utworzony moduł równoważenia obciążenia i dołączyć tooit maszyn wirtualnych. W tym samouczku omówiono:

> [!div class="checklist"]
> * Tworzenie usługi równoważenia obciążenia Azure
> * Utwórz kondycji sondę modułu równoważenia obciążenia
> * Tworzenie reguły ruchu usługi równoważenia obciążenia
> * Użyj hello niestandardowe rozszerzenie skryptu toocreate podstawowej witryny usług IIS
> * Tworzenie maszyn wirtualnych i Dołącz tooa modułu równoważenia obciążenia
> * Wyświetl modułu równoważenia obciążenia w akcji
> * Dodawanie i usuwanie maszyny wirtualne z modułem równoważenia obciążenia

Jak przejść dalej toolearn samouczka toohello toomanage sieci maszyny Wirtualnej.

> [!div class="nextstepaction"]
> [Zarządzanie maszynami wirtualnymi i sieciami wirtualnymi](./tutorial-virtual-network.md)
