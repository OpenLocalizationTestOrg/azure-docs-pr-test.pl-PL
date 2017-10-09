---
title: "aaaTutorial - kompilacji wysoką dostępność aplikacji na maszynach wirtualnych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate wysokiej dostępności i bezpieczne aplikacji w trzech maszyn wirtualnych systemu Windows z usługą równoważenia obciążenia na platformie Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 03/30/2017
ms.author: davidmu
ms.openlocfilehash: f9eff96be4f3999651c4108f0334e4eaa1a39c0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a>Tworzenie równoważone, wysoką dostępność aplikacji na maszynach wirtualnych systemu Windows na platformie Azure

W tym samouczku utworzysz wysokiej dostępności aplikacji, która jest odporność toomaintenance zdarzenia. Aplikacja Hello używa modułu równoważenia obciążenia, zestawu dostępności i trzech maszyn wirtualnych systemu Windows (VM). W tym samouczku instaluje usługi IIS, chociaż można użyć tego samouczka toodeploy framework innej aplikacji przy użyciu hello same składniki wysokiej dostępności i wytyczne. 

## <a name="step-1---azure-prerequisites"></a>Krok 1 — wymagania wstępne platformy Azure

toocomplete tego samouczka, upewnij się, czy hello zostały zainstalowane najnowsze [programu Azure PowerShell](/powershell/azure/overview) modułu.

Po pierwsze Zaloguj się za tooyour subskrypcji platformy Azure z hello polecenia Login-AzureRmAccount i wykonaj hello wyświetlanymi instrukcjami.

```powershell
Login-AzureRmAccount
```

Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi. Przed utworzeniem innych zasobów platformy Azure, należy toocreate grupą zasobów o [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `westeurope` regionu: 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a>Krok 2 — Tworzenie zestawu dostępności

Maszyny wirtualne mogą być tworzone przez błędów logicznych i Aktualizacja domeny. Każdej domeny logicznej reprezentuje część sprzętu w centrum danych Azure podstawowej hello. Po utworzeniu co najmniej dwie maszyny wirtualne, zasobów obliczeniowych i przestrzeni dyskowej są dystrybuowane w tych domenach. Tej dystrybucji przechowuje hello dostępność aplikacji, jeśli składnik sprzętowy wymaga konserwacji. Zestawy dostępności umożliwiają zdefiniowanie tych logicznej domen błędów i aktualizacji.

Utwórz zestaw o dostępności [AzureRmAvailabilitySet nowy](/powershell/module/azurerm.compute/new-azurermavailabilityset). Witaj poniższy przykład tworzy zbiór nazwanego dostępności `myAvailabilitySet`:

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a>Krok 3 — Tworzenie obciążenia równoważenia

Moduł równoważenia obciążenia Azure dystrybuuje ruch zestawu zdefiniowanego maszyn wirtualnych przy użyciu reguły modułu równoważenia obciążenia. Sondy kondycji monitoruje danego portu na każdej maszynie Wirtualnej, a tylko dystrybuuje ruch tooan operacyjne maszyny Wirtualnej.

### <a name="create-public-ip-address"></a>Utwórz publiczny adres IP

tooaccess aplikacji na powitania Internet, przypisz publicznego równoważenia obciążenia toohello adresów IP. Utwórz publiczny adres IP z [AzureRmPublicIpAddress nowy](/powershell/module/azurerm.network/new-azurermpublicipaddress). Witaj poniższy przykład tworzy publiczny adres IP o nazwie `myPublicIP`:

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a>Tworzenie usługi równoważenia obciążenia

Utwórz na adres IP frontonu [AzureRmLoadBalancerFrontendIpConfig nowy](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig). Witaj poniższy przykład tworzy adresu IP serwera sieci Web o nazwie `myFrontEndPool`: 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

Utwórz pulę adresów zaplecza z [AzureRmLoadBalancerBackendAddressPoolConfig nowy](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig). Witaj poniższy przykład tworzy puli adresów zaplecza, o nazwie `myBackEndPool`:

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

Teraz utworzymy hello modułu równoważenia obciążenia z [AzureRmLoadBalancer nowy](/powershell/module/azurerm.network/new-azurermloadbalancer). Witaj poniższy przykład tworzy moduł równoważenia obciążenia o nazwie `myLoadBalancer` przy użyciu hello `myPublicIP` adres:

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a>Utworzyć sondy kondycji

tooallow hello stanu usługi równoważenia obciążenia toomonitor hello aplikacji, możesz użyć sondy kondycji. sondy kondycji Hello dynamicznie dodaje lub usuwa maszyn wirtualnych z obrotu usługi równoważenia obciążenia hello oparte na ich kontroli toohealth odpowiedzi. Domyślnie maszyny Wirtualnej zostanie usunięte z dystrybucji modułu równoważenia obciążenia powitania po dwóch kolejnych błędów na 15 sekund.

Utwórz badanie kondycji z [AzureRmLoadBalancerProbeConfig Dodaj](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig). Witaj poniższy przykład tworzy badanie kondycji o nazwie `myHealthProbe` który monitoruje każdej maszyny Wirtualnej:

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a>Tworzenie reguły modułu równoważenia obciążenia

Reguły modułu równoważenia obciążenia jest używany toodefine sposób ruch jest rozproszonej toohello maszyn wirtualnych.

Tworzenie reguły modułu równoważenia obciążenia z [AzureRmLoadBalancerRuleConfig Dodaj](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig). Witaj poniższy przykład tworzy regułę równoważenia obciążenia o nazwie `myLoadBalancerRule` i równoważy ruch na porcie `80`:

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

Zaktualizuj hello modułu równoważenia obciążenia z [AzureRmLoadBalancer zestaw](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a>Krok 4 — Konfigurowanie sieci

Każda maszyna wirtualna ma co najmniej jeden wirtualny kart interfejsu sieciowego (NIC) łączących tooa sieci wirtualnej. Ta sieć wirtualna jest chroniona toofilter ruchu na podstawie reguł zdefiniowanych dostępu.

### <a name="create-virtual-network"></a>Tworzenie sieci wirtualnej

Skonfiguruj podsieci z [AzureRmVirtualNetworkSubnetConfig nowy](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig). Witaj poniższy przykład tworzy podsieć o nazwie `mySubnet`:

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

tooyour łączności sieciowej tooprovide maszyn wirtualnych, Utwórz sieć wirtualną z [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). Witaj poniższy przykład tworzy sieć wirtualną o nazwie `myVnet` z `mySubnet`:

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a>Konfigurowanie zabezpieczeń sieci

Azure [sieciowej grupy zabezpieczeń](../../virtual-network/virtual-networks-nsg.md) (NSG) steruje ruchu przychodzącego i wychodzącego dla jednego lub wielu maszyn wirtualnych. Reguły grupy zabezpieczeń sieci akceptować lub odrzucać ruchu sieciowego na określonym porcie lub zakres portów. Te zasady mogą również obejmować prefiks adresu źródłowego, dzięki czemu tylko ruch w źródle wstępnie zdefiniowanych może komunikować się z maszyną wirtualną.

tooallow aplikacji sieci web tooreach ruchu, należy utworzyć reguły grupy zabezpieczeń sieci z [AzureRmNetworkSecurityRuleConfig nowy](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig). Witaj poniższy przykład tworzy regułę grupy zabezpieczeń sieci o nazwie `myNetworkSecurityGroupRule`:

```powershell
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
```

Utwórz grupę zabezpieczeń sieci z [AzureRmNetworkSecurityGroup nowy](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup). Witaj poniższy przykład tworzy grupy NSG o nazwie `myNetworkSecurityGroup`:

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

Dodaj podsieć toohello grupy zabezpieczeń sieci hello z [AzureRmVirtualNetworkSubnetConfig zestaw](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

Aktualizacja sieci wirtualnej hello o [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a>Utwórz sieć wirtualną kartami interfejsu

Ładowanie funkcji równoważenia z hello wirtualnej karty Sieciowej zasobów zamiast hello rzeczywiste maszyny Wirtualnej. Hello wirtualnej karty Sieciowej podłączonej toohello Usługa równoważenia obciążenia, a następnie dołączony tooa maszyny Wirtualnej.

Tworzenie wirtualnej karty Sieciowej z [AzureRmNetworkInterface nowy](/powershell/module/azurerm.network/new-azurermnetworkinterface). Witaj poniższy przykład tworzy trzy wirtualne karty sieciowe. (Jedną wirtualną kartę Sieciową dla każdej maszyny Wirtualnej jest tworzona dla aplikacji w hello następujące kroki):


```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface -ResourceGroupName myResourceGroup `
     -Name myNic$i `
     -Location westeurope `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}

```

## <a name="step-5---create-virtual-machines"></a>Krok 5 — Tworzenie maszyn wirtualnych

Z wszystkich hello podstawowych składników w miejscu można teraz utworzyć toorun maszyn wirtualnych wysokiej dostępności aplikacji. 

Pobierz hello nazwę użytkownika i hasło potrzebne do konta administratora hello na maszynie wirtualnej hello [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Tworzenie maszyn wirtualnych hello z [AzureRmVMConfig nowy](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [AzureRmVMOperatingSystem zestaw](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [AzureRmVMSourceImage zestaw](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Dodać AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), i [nowe AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). Witaj poniższy przykład tworzy trzech maszyn wirtualnych:

```powershell
for ($i=1; $i -le 3; $i++)
{
   $vm = New-AzureRmVMConfig -VMName myVM$i -VMSize Standard_D1 -AvailabilitySetId $availabilitySet.Id
   $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName myVM$i -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version latest
   $vm = Set-AzureRmVMOSDisk -VM $vm -Name myOsDisk$i -StorageAccountType StandardLRS -DiskSizeInGB 128 -CreateOption FromImage -Caching ReadWrite
   $nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic$i
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vm
}

```

Go zajmuje kilka minut toocreate i skonfiguruj wszystkie trzy maszyny wirtualne. Witaj sondy kondycji modułu równoważenia obciążenia automatycznie wykrywa aplikacji hello jest uruchomiona na każdej maszynie Wirtualnej. Po uruchomieniu aplikacji hello reguły modułu równoważenia obciążenia hello uruchamia toodistribute ruchu.

### <a name="install-hello-app"></a>Instalowanie aplikacji hello 

Zadania konfiguracji maszyny wirtualnej tooautomate używane, takie jak instalowanie aplikacji i konfigurowanie systemu operacyjnego hello są rozszerzenia maszyny wirtualnej platformy Azure. Witaj [niestandardowe rozszerzenie skryptu dla systemu Windows](./../virtual-machines-windows-extensions-customscript.md) jest używane toorun dowolny skrypt programu PowerShell na maszynie wirtualnej hello. skrypt Hello można przechowywane w magazynie Azure, wszelkie dostępny punkt końcowy HTTP lub osadzone w konfiguracji rozszerzenia niestandardowego skryptu hello. Używając hello niestandardowe rozszerzenie skryptu, agent maszyny Wirtualnej Azure hello zarządza hello wykonywanie skryptu.

Użyj [AzureRmVMExtension zestaw](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello niestandardowego rozszerzenia skryptu. Witaj uruchamia rozszerzenia `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS serwer sieci Web:

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server"}' `
     -Location westeurope
}
```

### <a name="test-your-app"></a>Testowanie aplikacji

Uzyskaj hello publicznego adresu IP z usługi równoważenia obciążenia z [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Witaj poniższy przykład uzyskuje hello adres IP dla `myPublicIP` utworzony wcześniej:

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

Wprowadź hello publicznego adresu IP w przeglądarce sieci web tooa. Reguły NSG hello w miejscu hello domyślna witryna sieci Web IIS są wyświetlane. 

![Domyślna witryna usług IIS](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a>Krok 6 — zadania związane z zarządzaniem

Może być konieczne tooperform konserwacji na powitania maszyn wirtualnych z tą aplikacją, takich jak instalowanie aktualizacji systemu operacyjnego. toodeal z aplikacją tooyour zwiększenie obciążenia, może być konieczne tooadd kolejnych maszyn wirtualnych. W tej sekcji opisano sposób tooremove lub dodać maszyny Wirtualnej z hello modułu równoważenia obciążenia. 

### <a name="remove-a-vm-from-hello-load-balancer"></a>Usuń Maszynę wirtualną z hello modułu równoważenia obciążenia

Usuń Maszynę wirtualną z puli adresów zaplecza hello resetując właściwość Loadbalancerbackendaddresspool hello hello karty sieciowej.

Pobierz hello karty interfejsu sieciowego z [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

Ustaw właściwość Loadbalancerbackendaddresspool hello karty interfejsu sieciowego hello zbyt$ null:

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

Karty interfejsu sieciowego hello aktualizacji:

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-toohello-load-balancer"></a>Dodaj usługi równoważenia obciążenia toohello maszyny Wirtualnej

Po konserwacja maszyny Wirtualnej lub tooexpand pojemności należy dodawanie hello karty Sieciowej maszyny Wirtualnej puli adresów zaplecza toohello hello usługi równoważenia obciążenia.

Pobierz hello usługi równoważenia obciążenia:

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

Dodaj hello puli adresów zaplecza modułu równoważenia obciążenia hello toohello karty interfejsu sieciowego:

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

Karty interfejsu sieciowego hello aktualizacji:

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a>Następne kroki

Przykłady — [programu Azure PowerShell maszyny wirtualnej przykładowe skrypty](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
