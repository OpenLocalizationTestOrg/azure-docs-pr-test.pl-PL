---
title: "Samouczek — kompilacji wysoką dostępność aplikacji na maszynach wirtualnych Azure | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie tworzenia aplikacji wysokiej dostępności i bezpieczne w trzech maszyn wirtualnych systemu Windows z usługą równoważenia obciążenia na platformie Azure"
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
ms.openlocfilehash: 4b8690a11ec0e711782a112622e1193c24292289
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a>Tworzenie równoważone, wysoką dostępność aplikacji na maszynach wirtualnych systemu Windows na platformie Azure

W tym samouczku utworzysz wysokiej dostępności aplikacji, która jest odporność obsługi zdarzeń. Aplikacja korzysta z modułu równoważenia obciążenia, zestawu dostępności i trzech maszyn wirtualnych systemu Windows (VM). W tym samouczku instaluje usługi IIS, chociaż można użyć w tym samouczku framework innej aplikacji, przy użyciu tego samego składniki wysokiej dostępności i wskazówki dotyczące wdrażania. 

## <a name="step-1---azure-prerequisites"></a>Krok 1 — wymagania wstępne platformy Azure

Do ukończenia tego samouczka, upewnij się, że zainstalowano najnowszą [programu Azure PowerShell](/powershell/azure/overview) modułu.

Najpierw należy zalogować się do Twojej subskrypcji platformy Azure przy użyciu polecenia Login-AzureRmAccount i postępuj zgodnie z wyświetlanymi instrukcjami.

```powershell
Login-AzureRmAccount
```

Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi. Przed utworzeniem innych zasobów platformy Azure, musisz utworzyć nową grupę zasobów o [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w `westeurope` regionu: 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a>Krok 2 — Tworzenie zestawu dostępności

Maszyny wirtualne mogą być tworzone przez błędów logicznych i Aktualizacja domeny. Każdej domeny logicznej reprezentuje część sprzętu w podstawowej centrum danych Azure. Po utworzeniu co najmniej dwie maszyny wirtualne, zasobów obliczeniowych i przestrzeni dyskowej są dystrybuowane w tych domenach. Tej dystrybucji przechowuje dostępność aplikacji, jeśli składnik sprzętowy wymaga konserwacji. Zestawy dostępności umożliwiają zdefiniowanie tych logicznej domen błędów i aktualizacji.

Utwórz zestaw o dostępności [AzureRmAvailabilitySet nowy](/powershell/module/azurerm.compute/new-azurermavailabilityset). Poniższy przykład tworzy zbiór nazwanego dostępności `myAvailabilitySet`:

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

Moduł równoważenia obciążenia Azure dystrybuuje ruch zestawu zdefiniowanego maszyn wirtualnych przy użyciu reguły modułu równoważenia obciążenia. Badania kondycji monitoruje danego portu na każdej maszynie Wirtualnej i tylko dystrybuuje ruch do operacyjnej maszyny Wirtualnej.

### <a name="create-public-ip-address"></a>Utwórz publiczny adres IP

Aby uzyskać dostęp do aplikacji w Internecie, należy przypisać publicznego adresu IP usługi równoważenia obciążenia. Utwórz publiczny adres IP z [AzureRmPublicIpAddress nowy](/powershell/module/azurerm.network/new-azurermpublicipaddress). Poniższy przykład tworzy publiczny adres IP o nazwie `myPublicIP`:

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a>Tworzenie usługi równoważenia obciążenia

Utwórz na adres IP frontonu [AzureRmLoadBalancerFrontendIpConfig nowy](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig). Poniższy przykład tworzy adresu IP serwera sieci Web o nazwie `myFrontEndPool`: 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

Utwórz pulę adresów zaplecza z [AzureRmLoadBalancerBackendAddressPoolConfig nowy](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig). Poniższy przykład tworzy puli adresów zaplecza, o nazwie `myBackEndPool`:

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

Teraz Utwórz moduł równoważenia obciążenia z [AzureRmLoadBalancer nowy](/powershell/module/azurerm.network/new-azurermloadbalancer). Poniższy przykład tworzy moduł równoważenia obciążenia o nazwie `myLoadBalancer` przy użyciu `myPublicIP` adres:

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a>Utworzyć sondy kondycji

Aby zezwolić usłudze równoważenia obciążenia do monitorowania stanu aplikacji, należy użyć sondy kondycji. Sondy kondycji dynamicznie dodaje lub usuwa maszyn wirtualnych z oparte na ich odpowiedzi na sprawdzenie kondycji obrót usługi równoważenia obciążenia. Domyślnie maszyny Wirtualnej zostanie usunięte z dystrybucji modułu równoważenia obciążenia po dwóch kolejnych błędów na 15 sekund.

Utwórz badanie kondycji z [AzureRmLoadBalancerProbeConfig Dodaj](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig). Poniższy przykład tworzy badanie kondycji o nazwie `myHealthProbe` który monitoruje każdej maszyny Wirtualnej:

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a>Tworzenie reguły modułu równoważenia obciążenia

Reguły modułu równoważenia obciążenia jest używany do definiowania rozkład ruchu do maszyn wirtualnych.

Tworzenie reguły modułu równoważenia obciążenia z [AzureRmLoadBalancerRuleConfig Dodaj](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig). Poniższy przykład tworzy regułę równoważenia obciążenia o nazwie `myLoadBalancerRule` i równoważy ruch na porcie `80`:

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

Aktualizacja usługi równoważenia obciążenia z [AzureRmLoadBalancer zestaw](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a>Krok 4 — Konfigurowanie sieci

Każda maszyna wirtualna ma co najmniej jeden wirtualny kart interfejsu sieciowego (NIC) łączących się z siecią wirtualną. Ta sieć wirtualna jest chroniona do filtrowania ruchu na podstawie reguł zdefiniowanych dostępu.

### <a name="create-virtual-network"></a>Tworzenie sieci wirtualnej

Skonfiguruj podsieci z [AzureRmVirtualNetworkSubnetConfig nowy](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig). Poniższy przykład tworzy podsieć o nazwie `mySubnet`:

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

Aby zapewnić łączność sieciową dla maszyn wirtualnych, Utwórz sieć wirtualną z [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). Poniższy przykład tworzy sieć wirtualną o nazwie `myVnet` z `mySubnet`:

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

Aby zezwolić na ruch w sieci web do aplikacji, należy utworzyć reguły grupy zabezpieczeń sieci z [AzureRmNetworkSecurityRuleConfig nowy](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig). Poniższy przykład tworzy regułę grupy zabezpieczeń sieci o nazwie `myNetworkSecurityGroupRule`:

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

Utwórz grupę zabezpieczeń sieci z [AzureRmNetworkSecurityGroup nowy](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup). Poniższy przykład tworzy grupy NSG o nazwie `myNetworkSecurityGroup`:

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

Dodaj sieciową grupę zabezpieczeń do podsieci o [AzureRmVirtualNetworkSubnetConfig zestaw](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

Aktualizacja sieci wirtualnej z [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a>Utwórz sieć wirtualną kartami interfejsu

Załadować funkcji równoważenia zasobu wirtualnego karty Sieciowej, a nie rzeczywiste maszyny Wirtualnej. Wirtualnej karty Sieciowej jest połączone z usługą równoważenia obciążenia, a następnie dołączony do maszyny Wirtualnej.

Tworzenie wirtualnej karty Sieciowej z [AzureRmNetworkInterface nowy](/powershell/module/azurerm.network/new-azurermnetworkinterface). Poniższy przykład tworzy trzy wirtualne karty sieciowe. (Jedną wirtualną kartę Sieciową dla każdej maszyny Wirtualnej jest tworzona dla aplikacji w poniższych krokach):


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

Wszystkie składniki w miejscu można teraz tworzyć maszyny wirtualne o wysokiej dostępności do uruchomienia aplikacji sieci. 

Pobierz nazwę użytkownika i hasło potrzebne do konta administratora na maszynie wirtualnej z [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Tworzenie maszyn wirtualnych o [nowe AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [AzureRmVMOperatingSystem zestaw](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [AzureRmVMSourceImage zestaw](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [AzureRmVMOSDisk zestaw](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [AzureRmVMNetworkInterface dodać](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), i [nowe AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). Poniższy przykład tworzy trzech maszyn wirtualnych:

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

Trwa kilka minut, aby utworzyć i skonfigurować wszystkie trzy maszyny wirtualne. Sondy kondycji modułu równoważenia obciążenia automatycznie wykrywa, gdy aplikacja jest uruchomiona na każdej maszynie Wirtualnej. Gdy aplikacja jest uruchomiona, rozpoczyna się reguły modułu równoważenia obciążenia do dystrybucji ruchu.

### <a name="install-the-app"></a>Zainstaluj aplikację 

Rozszerzenia maszyny wirtualnej platformy Azure są używane do automatyzowania zadań konfiguracji maszyny wirtualnej, takie jak instalowanie aplikacji i konfigurowanie systemu operacyjnego. [Niestandardowe rozszerzenie skryptu dla systemu Windows](./../virtual-machines-windows-extensions-customscript.md) służy do uruchomienia dowolnego skryptu programu PowerShell na maszynie wirtualnej. Skrypt można przechowywane w magazynie Azure, wszelkie dostępny punkt końcowy HTTP lub osadzone w konfiguracji rozszerzenia niestandardowego skryptu. Podczas korzystania z niestandardowego rozszerzenia skryptu, agent maszyny Wirtualnej platformy Azure zarządza wykonania skryptu.

Użyj [AzureRmVMExtension zestaw](/powershell/module/azurerm.compute/set-azurermvmextension) można zainstalować rozszerzenia niestandardowego skryptu. Uruchamia rozszerzenia `powershell Add-WindowsFeature Web-Server` Aby zainstalować serwer sieci Web usług IIS:

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

Publiczny adres IP z usługi równoważenia obciążenia z [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Poniższy przykład uzyskuje adres IP dla `myPublicIP` utworzony wcześniej:

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

Wprowadź publicznego adresu IP w przeglądarce sieci web. Reguły NSG w miejscu wyświetlane jest IIS domyślnej witryny sieci Web. 

![Domyślna witryna usług IIS](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a>Krok 6 — zadania związane z zarządzaniem

Może być konieczne przeprowadzenie konserwacji na maszynach wirtualnych z tą aplikacją, takich jak instalowanie aktualizacji systemu operacyjnego. Aby poradzić sobie z zwiększenie obciążenia do aplikacji, może być konieczne dodanie kolejnych maszyn wirtualnych. W tej sekcji przedstawiono sposób Usuń lub Dodaj Maszynę wirtualną z modułu równoważenia obciążenia. 

### <a name="remove-a-vm-from-the-load-balancer"></a>Usuń Maszynę wirtualną z usługi równoważenia obciążenia

Usuń Maszynę wirtualną z puli adresów zaplecza resetując właściwość Loadbalancerbackendaddresspool karty interfejsu sieciowego.

Pobierz karty interfejsu sieciowego z [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

Ustaw właściwość Loadbalancerbackendaddresspool karty interfejsu sieciowego na $null:

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

Aktualizacja karty interfejsu sieciowego:

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-to-the-load-balancer"></a>Dodaj Maszynę wirtualną z usługą równoważenia obciążenia

Po konserwacja maszyny Wirtualnej, lub jeśli trzeba zwiększyć pojemność, dodanie karty Sieciowej maszyny wirtualnej do puli adresów zaplecza modułu równoważenia obciążenia.

Pobierz moduł równoważenia obciążenia:

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

Dodaj puli adresów zaplecza modułu równoważenia obciążenia do karty interfejsu sieciowego:

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

Aktualizacja karty interfejsu sieciowego:

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a>Następne kroki

Przykłady — [programu Azure PowerShell maszyny wirtualnej przykładowe skrypty](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
