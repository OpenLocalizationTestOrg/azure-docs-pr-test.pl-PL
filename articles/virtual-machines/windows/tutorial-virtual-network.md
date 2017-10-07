---
title: aaaAzure sieci wirtualnych i maszyn wirtualnych z systemem Windows | Dokumentacja firmy Microsoft
description: "Samouczek — Zarządzanie sieciami wirtualnymi platformy Azure i maszyn wirtualnych z systemem Windows przy użyciu programu Azure PowerShell"
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
ms.date: 05/02/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: ed77d9d5873e849fcb2aaf15e41899d7ad8c781a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a>Zarządzanie sieciami wirtualnymi platformy Azure i maszyn wirtualnych z systemem Windows przy użyciu programu Azure PowerShell

Maszyny wirtualne platformy Azure używania sieci platformy Azure do komunikacji sieciowej wewnętrznych i zewnętrznych. W tym samouczku należy utworzyć wiele maszyn wirtualnych (VM) w sieci wirtualnej i skonfigurować łączność sieciową między nimi. Omawiane kwestie:

> [!div class="checklist"]
> * Tworzenie sieci wirtualnej
> * Tworzenie podsieci sieci wirtualnej
> * Kontrola ruchu sieciowego z grup zabezpieczeń sieci
> * Widok reguły ruchu w akcji

Ten samouczek wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej. Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji. Jeśli potrzebujesz tooupgrade, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="create-vnet"></a>Tworzenie sieci wirtualnej

Sieci wirtualnej jest reprezentację sieci w chmurze hello. Sieci wirtualnej jest logiczną izolacją hello subskrypcji tooyour chmury Azure w wersji dedykowanej. W ramach sieci wirtualnej można znaleźć podsieci, zasad łączności toothose podsieci i połączeń z podsieciami toohello maszyn wirtualnych hello.

Przed utworzeniem innych zasobów platformy Azure, należy toocreate grupą zasobów o [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Witaj poniższy przykład tworzy grupę zasobów o nazwie *myRGNetwork* w hello *EastUS* lokalizacji:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

Podsieć jest zasobem podrzędnych sieci wirtualnej i pomaga zdefiniować segmenty przestrzeni adresów w obrębie blok CIDR, przy użyciu prefiksów adresów IP. Karty sieciowe mogą być dodawane toosubnets i tooVMs połączone, zapewniają łączność dla różnych obciążeń.

Utwórz podsieć o [AzureRmVirtualNetworkSubnetConfig nowy](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

Tworzenie sieci Wirtualnej o nazwie *myVNet* przy użyciu *myFrontendSubnet* z [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a>Tworzenie maszyny Wirtualnej z frontonu

Toocommunicate maszyny Wirtualnej w sieci wirtualnej musi on interfejs sieci wirtualnej (NIC). Witaj *myFrontendVM* jest dostępny z hello internetowe, dlatego też potrzebuje publicznego adresu IP. 

Utwórz publiczny adres IP z [AzureRmPublicIpAddress nowy](/powershell/module/azurerm.network/new-azurermpublicipaddress):

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

Utwórz kartę Sieciową z [nowe AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

Ustaw hello nazwę użytkownika i hasło potrzebne do konta administratora hello na powitania maszyny Wirtualnej z [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Tworzenie maszyn wirtualnych hello z [AzureRmVMConfig nowy](/powershell/module/azurerm.compute/new-azurermvmconfig), [AzureRmVMOperatingSystem zestaw](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [AzureRmVMSourceImage zestaw](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Dodać AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), i [nowe AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). 

```powershell
$frontendVM = New-AzureRmVMConfig `
    -VMName myFrontendVM `
    -VMSize Standard_D1
$frontendVM = Set-AzureRmVMOperatingSystem `
    -VM $frontendVM `
    -Windows `
    -ComputerName myFrontendVM `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
$frontendVM = Set-AzureRmVMSourceImage `
    -VM $frontendVM `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
$frontendVM = Set-AzureRmVMOSDisk `
    -VM $frontendVM `
    -Name myFrontendOSDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
$frontendVM = Add-AzureRmVMNetworkInterface `
    -VM $frontendVM `
    -Id $frontendNic.Id
New-AzureRmVM `
    -ResourceGroupName myRGNetwork `
    -Location EastUS `
    -VM $frontendVM
```

## <a name="install-web-server"></a>Zainstaluj serwer sieci web

Można zainstalować usługi IIS na *myFrontendVM* przy użyciu sesji pulpitu zdalnego. Należy tooget hello publicznego adresu IP hello wirtualna tooaccess go.

Można uzyskać hello publicznego adresu IP *myFrontendVM* z [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Witaj poniższy przykład uzyskuje hello adres IP dla *myPublicIPAddress* utworzony wcześniej:

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

Zwróć uwagę, ten adres IP, dzięki czemu można używać w przyszłości czynności.

Użyj hello następujące polecenie toocreate sesję pulpitu zdalnego z *myFrontendVM*. Zastąp  *<publicIPAddress>*  z adresem hello uprzednio zarejestrowane. Po wyświetleniu monitu wprowadź poświadczenia hello przy tworzeniu hello maszyny Wirtualnej.

```
mstsc /v:<publicIpAddress>
``` 

Teraz, gdy użytkownik zalogował się za*myFrontendVM*, można użyć pojedynczy wiersz tooinstall PowerShell usług IIS i włączyć ruchu tooallow reguły hello lokalnej zapory w sieci web. Otwórz wiersz programu PowerShell i uruchom następujące polecenie hello:

Użyj [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun hello niestandardowe rozszerzenie skryptu, który instaluje serwer sieci Web usług IIS hello:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

Teraz można używać hello publicznego adresu IP adres toobrowse toohello wirtualna toosee hello witryny usług IIS.

![Domyślna witryna usług IIS](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a>Zarządzanie ruchem wewnętrzny

Grupa zabezpieczeń sieci (NSG) zawiera listę reguł zabezpieczeń, które lub odmawiają tooa tooresources połączone ruchu sieci wirtualnej. Grupy NSG mogą być skojarzone toosubnets lub tooVMs dołączony poszczególnymi kartami sieciowymi. Otwarcie lub zamknięcie tooVMs dostęp za pośrednictwem portów jest wykonywane przy użyciu reguły NSG. Podczas tworzenia *myFrontendVM*, przychodzący port 3389 automatycznie zostało otwarte połączenia RDP.

Za pomocą grupy NSG można skonfigurować komunikację wewnętrzną maszyn wirtualnych. W tej sekcji omówiono sposób toocreate dodatkowe podsieci w hello sieciowe i przypisz tooallow tooit NSG połączenia z *myFrontendVM* za*myBackendVM* na porcie 1433. podsieci Hello jest przypisywana toohello maszyny Wirtualnej po jej utworzeniu.

Można ograniczyć ruch wewnętrzny zbyt*myBackendVM* tylko od *myFrontendVM* przez utworzenie grupy NSG podsieci wewnętrznej hello. Witaj poniższy przykład tworzy reguły NSG o nazwie *myBackendNSGRule* z [AzureRmNetworkSecurityRuleConfig nowy](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):

```powershell
$nsgBackendRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myBackendNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 100 `
  -SourceAddressPrefix 10.0.0.0/24 `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 1433 `
  -Access Allow
```

Dodaj sieciową grupę zabezpieczeń o nazwie *myBackendNSG* z [AzureRmNetworkSecurityGroup nowy](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a>Dodaj podsieć zaplecza

Dodaj *myBackEndSubnet* za*myVNet* z [AzureRmVirtualNetworkSubnetConfig Dodaj](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):

```powershell
Add-AzureRmVirtualNetworkSubnetConfig `
  -Name myBackendSubnet `
  -VirtualNetwork $vnet `
  -AddressPrefix 10.0.1.0/24 `
  -NetworkSecurityGroup $nsgBackend
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
$vnet = Get-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Name myVNet
```

## <a name="create-back-end-vm"></a>Tworzenie maszyny Wirtualnej z zaplecza

Witaj Najprostszym sposobem toocreate Witaj zaplecza maszyny Wirtualnej jest przy użyciu obrazu programu SQL Server. W tym samouczku tylko tworzy hello maszyny Wirtualnej z serwerem bazy danych hello, ale nie dostarcza informacji na temat uzyskiwania dostępu do bazy danych hello.

Utwórz *myBackendNic*:

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

Ustaw hello nazwę użytkownika i hasło potrzebne do konta administratora hello na powitania maszyny Wirtualnej z Get-Credential:

```powershell
$cred = Get-Credential
```

Utwórz *myBackendVM*:

```powershell
$backendVM = New-AzureRmVMConfig `
  -VMName myBackendVM `
  -VMSize Standard_D1
$backendVM = Set-AzureRmVMOperatingSystem `
  -VM $backendVM `
  -Windows `
  -ComputerName myBackendVM `
  -Credential $cred `
  -ProvisionVMAgent `
  -EnableAutoUpdate
$backendVM = Set-AzureRmVMSourceImage `
  -VM $backendVM `
  -PublisherName MicrosoftSQLServer `
  -Offer SQL2016SP1-WS2016 `
  -Skus Enterprise `
  -Version latest
$backendVM = Set-AzureRmVMOSDisk `
  -VM $backendVM `
  -Name myBackendOSDisk `
  -DiskSizeInGB 128 `
  -CreateOption FromImage `
  -Caching ReadWrite
$backendVM = Add-AzureRmVMNetworkInterface `
  -VM $backendVM `
  -Id $backendNic.Id
New-AzureRmVM `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -VM $backendVM
```

Obraz powitania, który jest używany zainstalowany program SQL Server, ale nie jest używana w tym samouczku. Jest dołączony tooshow możesz sposobu konfigurowania ruchu w sieci web toohandle maszyny Wirtualnej i zarządzania bazy danych toohandle maszyny Wirtualnej.

## <a name="next-steps"></a>Następne kroki

W tym samouczku zostało utworzone i zabezpieczonej sieci platformy Azure jako powiązane toovirtual maszyny. 

> [!div class="checklist"]
> * Tworzenie sieci wirtualnej
> * Tworzenie podsieci sieci wirtualnej
> * Kontrola ruchu sieciowego z grup zabezpieczeń sieci
> * Widok reguły ruchu w akcji

Przejdź dalej toolearn samouczka toohello o monitorowaniu Zabezpieczanie danych w przypadku maszyn wirtualnych przy użyciu kopii zapasowej systemu Azure. .

> [!div class="nextstepaction"]
> [Tworzenie kopii zapasowych maszyn wirtualnych systemu Windows na platformie Azure](./tutorial-backup-vms.md)
