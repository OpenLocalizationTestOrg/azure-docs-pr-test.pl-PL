---
title: "aaaCreate i zarządzania maszynami wirtualnymi systemu Windows z hello modułu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Samouczek — tworzenie i zarządzanie maszynami wirtualnymi systemu Windows z hello modułu Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 20adcb673ef4de683e6ad82d048a9625a1dc838c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-with-hello-azure-powershell-module"></a>Tworzenie i zarządzanie maszynami wirtualnymi systemu Windows z hello modułu Azure PowerShell

Maszyny wirtualne platformy Azure zawierają w pełni konfigurowalne i elastyczne środowiska komputerowego. Ten samouczek obejmuje elementów wdrożenia podstawowej maszyny wirtualnej platformy Azure, takich jak rozmiar maszyny Wirtualnej, wybierając obrazu maszyny Wirtualnej i wdrażanie maszyny Wirtualnej. Omawiane kwestie:

> [!div class="checklist"]
> * Tworzenie i łączenie tooa maszyny Wirtualnej
> * Wybierz i używać obrazów maszyn wirtualnych
> * Wyświetlanie i używanie określonych rozmiarów maszyn wirtualnych
> * Zmienianie rozmiaru maszyny wirtualnej
> * Wyświetlanie i zrozumienie stanu maszyny Wirtualnej

Ten samouczek wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej. Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji. Jeśli potrzebujesz tooupgrade, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="create-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów o hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) polecenia. 

Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi. Grupy zasobów musi zostać utworzone przed maszyny wirtualnej. W tym przykładzie grupy zasobów o nazwie *myResourceGroupVM* jest tworzony w hello *EastUS* regionu. 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

Grupa zasobów Hello jest określony, podczas tworzenia lub modyfikowania maszyn wirtualnych, które są widoczne w tym samouczku.

## <a name="create-virtual-machine"></a>Tworzenie maszyny wirtualnej

Maszyna wirtualna musi być tooa połączonych sieci wirtualnej. Do komunikacji z maszyny wirtualnej hello za pomocą publicznego adresu IP za pośrednictwem karty interfejsu sieciowego.

### <a name="create-virtual-network"></a>Tworzenie sieci wirtualnej

Utwórz podsieć o [AzureRmVirtualNetworkSubnetConfig nowy](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

Tworzenie sieci wirtualnej z [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a>Utwórz publiczny adres IP

Utwórz publiczny adres IP z [AzureRmPublicIpAddress nowy](/powershell/module/azurerm.network/new-azurermpublicipaddress):

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a>Utwórz karty interfejsu sieciowego

Utwórz kartę sieciową z [AzureRmNetworkInterface nowy](/powershell/module/azurerm.network/new-azurermnetworkinterface):

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a>Utwórz grupę zabezpieczeń sieci

Azure [sieciowej grupy zabezpieczeń](../../virtual-network/virtual-networks-nsg.md) (NSG) steruje ruchu przychodzącego i wychodzącego dla jednego lub wielu maszyn wirtualnych. Reguły grupy zabezpieczeń sieci akceptować lub odrzucać ruchu sieciowego na określonym porcie lub zakres portów. Te zasady mogą również obejmować prefiks adresu źródłowego, dzięki czemu tylko ruch w źródle wstępnie zdefiniowanych może komunikować się z maszyną wirtualną. tooaccess hello IIS serwer sieci Web, który jest instalowany, należy dodać regułę ruchu przychodzącego grupy NSG.

Użyj toocreate regułę ruchu przychodzącego grupy NSG [AzureRmNetworkSecurityRuleConfig Dodaj](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig). Witaj poniższy przykład tworzy reguły NSG o nazwie *myNSGRule* który otwiera port *3389* hello maszyny wirtualnej:

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1000 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 3389 `
  -Access Allow
```

Tworzenie przy użyciu NSG hello *myNSGRule* z [AzureRmNetworkSecurityGroup nowy](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

Dodaj hello NSG toohello podsieci w sieci wirtualnej hello o [AzureRmVirtualNetworkSubnetConfig zestaw](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

Aktualizacja sieci wirtualnej hello o [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a>Tworzenie maszyny wirtualnej

Podczas tworzenia maszyny wirtualnej, takich jak obraz systemu operacyjnego, dysku zmiany rozmiaru i administracyjnych poświadczeń jest kilka opcji. W tym przykładzie utworzono maszynę wirtualną o nazwie *myVM* uruchomionych hello najnowszej wersji systemu Windows Server 2016 Datacenter.

Ustaw hello nazwę użytkownika i hasło potrzebne do konta administratora hello na maszynie wirtualnej hello [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Utwórz hello konfiguracji początkowej dla maszyny wirtualnej hello o [AzureRmVMConfig nowy](/powershell/module/azurerm.compute/new-azurermvmconfig):

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

Dodaj hello systemu operacyjnego informacji toohello konfiguracji maszyny wirtualnej z [AzureRmVMOperatingSystem zestaw](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

Dodaj hello obrazu informacji toohello konfiguracji maszyny wirtualnej z [AzureRmVMSourceImage zestaw](/powershell/module/azurerm.compute/set-azurermvmsourceimage):

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

Dodaj hello systemu operacyjnego dysku ustawienia toohello konfiguracji maszyny wirtualnej z [AzureRmVMOSDisk zestaw](/powershell/module/azurerm.compute/set-azurermvmosdisk):

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

Dodaj hello kartom sieciowym wcześniej utworzony toohello konfiguracji maszyny wirtualnej z [AzureRmVMNetworkInterface Dodaj](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

Utwórz maszynę wirtualną hello z [AzureRmVM nowy](/powershell/module/azurerm.compute/new-azurermvm).

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-toovm"></a>Połącz tooVM

Po zakończeniu wdrożenia hello, tworzenia połączenia pulpitu zdalnego z maszyną wirtualną hello.

Uruchom następujące polecenia tooreturn hello publicznego adresu IP maszyny wirtualnej hello hello. Zwróć uwagę ten adres IP, więc tooit mogą łączyć się z tootest przeglądarki sieci web łączność w przyszłości kroku.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

Użyj hello następujące polecenie toocreate sesję pulpitu zdalnego z maszyną wirtualną hello. Zamień adres IP hello hello *publicznego adresu IP* maszyny wirtualnej. Po wyświetleniu monitu wprowadź poświadczenia hello używane podczas tworzenia maszyny wirtualnej hello.

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a>Zrozumienie obrazów maszyn wirtualnych

Hello Azure marketplace zawiera wiele obrazów maszyny wirtualnej, które mogą być używane toocreate nowej maszyny wirtualnej. W poprzednich krokach hello maszyny wirtualnej został utworzony przy użyciu obrazu systemu Windows Server 2016-Datacenter hello. W tym kroku hello modułu programu PowerShell jest używane toosearch hello marketplace dla innych obrazów systemu Windows, które może również jako podstawa dla nowych maszyn wirtualnych. Proces ten składa się z znajdowanie hello wydawcy, oferty i nazwa obrazu hello (Sku). 

Użyj hello [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) tooreturn polecenia listę wydawców obrazu.  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

Użyj hello [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn listę ofert obrazu. To polecenie hello zwracany lista jest przefiltrowana na powitania określonego wydawcę. 

```powershell
Get-AzureRmVMImageOffer -Location "EastUS" -PublisherName "MicrosoftWindowsServer"
```

```powershell
Offer             PublisherName          Location
-----             -------------          -------- 
Windows-HUB       MicrosoftWindowsServer EastUS 
WindowsServer     MicrosoftWindowsServer EastUS   
WindowsServer-HUB MicrosoftWindowsServer EastUS   
```

Witaj [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) polecenia zostanie następnie odfiltrować tooreturn nazwę wydawcy i oferty hello listę nazw obrazu.

```powershell
Get-AzureRmVMImageSku -Location "EastUS" -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer"
```

```powershell
Skus                            Offer         PublisherName          Location
----                            -----         -------------          --------
2008-R2-SP1                     WindowsServer MicrosoftWindowsServer EastUS  
2008-R2-SP1-BYOL                WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter-BYOL            WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter              WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter-BYOL         WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-Server-Core     WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-with-Containers WindowsServer MicrosoftWindowsServer EastUS  
2016-Nano-Server                WindowsServer MicrosoftWindowsServer EastUS
```

Te informacje mogą być używane toodeploy maszynę Wirtualną za pomocą określonego obrazu. W tym przykładzie nazwa obrazu hello na powitania obiektu maszyny Wirtualnej. W tym samouczku instrukcje ukończenia wdrożenia można znaleźć toohello poprzednich przykładach.

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a>Zrozumienie rozmiarów maszyn wirtualnych

Rozmiar maszyny wirtualnej określa hello zasobów obliczeniowych, takich jak Procesora GPU i pamięci wprowadzone toohello dostępne maszyny wirtualnej. Maszyny wirtualne muszą toobe utworzony z rozmiarem odpowiedniego dla hello oczekiwane obciążenia pracą. Jeśli zwiększa obciążenie, można zmienić rozmiar istniejącej maszyny wirtualnej.

### <a name="vm-sizes"></a>Rozmiary maszyn wirtualnych

w poniższej tabeli Hello kategoryzuje rozmiary do przypadków użycia.  

| Typ                     | Rozmiary           |    Opis       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| Zastosowania ogólne         |DSv2, Dv2, DS, D, Av2, A0 7| Zrównoważonym Procesora do pamięci. Nadaje się doskonale dla deweloperów / testu i małych toomedium rozwiązania aplikacji i danych.  |
| Optymalizacja pod kątem obliczeń      | FS, F             | Wysoka Procesora do pamięci. Nadaje się do aplikacji średnia ruchu, urządzeń sieciowych i procesów wsadowych.        |
| Optymalizacja pod kątem pamięci       | GS, G, DSv2, DS, Dv2, D   | Wysoka pamięci do core. Doskonałe rozwiązanie dla relacyjnych baz danych, pamięci podręcznych średnia toolarge i analiza w pamięci.                 |
| Optymalizacja pod kątem magazynu       | Ls                | Wysoka przepływność dysku i operacje we/wy. Idealne rozwiązanie w przypadku danych big data oraz baz danych SQL i NoSQL.                                                         |
| Procesory GPU           | WIRTUALIZACJĄ SIECI, NC            | Celem duże Renderowanie grafiki i wideo edycji specjalne maszyn wirtualnych.       |
| Wysoka wydajność | H-A8 11          | Nasze najbardziej zaawansowanych Procesora maszyny wirtualne z interfejsami opcjonalne wysokiej przepustowości sieci (RDMA). 


### <a name="find-available-vm-sizes"></a>Znajdowanie dostępnych rozmiarów maszyny Wirtualnej

toosee listę maszyn wirtualnych rozmiarów dostępnych w określonym regionie, użyj hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) polecenia.

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a>Zmienianie rozmiaru maszyny wirtualnej

Po wdrożeniu maszyny Wirtualnej można tooincrease po zmianie rozmiaru lub zmniejszenia alokacji zasobów.

Przed zmianą rozmiaru maszyny Wirtualnej, sprawdź, czy hello wymagany rozmiar w klastrze jest dostępny hello bieżącej maszyny Wirtualnej. Witaj [Get AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) polecenie zwraca listę rozmiarów. 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

W razie potrzeby hello się, że rozmiar jest dostępny hello maszyny Wirtualnej można zmienić rozmiar ze stanu zasilania na, jednak podczas hello operacji ponownego rozruchu.

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

Jeśli hello żądany rozmiar nie jest na powitania bieżący klaster hello wirtualna potrzeb, może wystąpić toobe alokację przed hello operacja zmiany rozmiaru. Uwaga: w przypadku hello maszyny Wirtualnej jest włączona ponownie, zostaną usunięte wszystkie dane na dysku tymczasowym hello i zmienić hello publicznego adresu IP, chyba że używana jest statyczny adres IP. 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a>Stany zasilania maszyny Wirtualnej

Maszyny Wirtualnej platformy Azure może mieć jedną z wielu stany zasilania. Ten stan reprezentuje hello bieżący stan hello maszyny Wirtualnej z punktu widzenia hello hello funkcji hypervisor. 

### <a name="power-states"></a>Stany zasilania

| Stan zasilania | Opis
|----|----|
| Uruchamianie | Wskazuje, że jest uruchamiana hello maszyny wirtualnej. |
| Działanie | Wskazuje, że działa hello maszyny wirtualnej. |
| Zatrzymywanie | Wskazuje, że tej maszyny wirtualnej hello jest zatrzymywana. | 
| Zatrzymane | Wskazuje, że tej maszyny wirtualnej hello jest zatrzymana. Należy pamiętać, że maszyny wirtualne w stanie hello zatrzymana nadal naliczenie opłat za obliczenia.  |
| Cofanie przydziału | Wskazuje, że cofana jest hello maszyny wirtualnej. |
| Cofnięcie przydziału | Wskazuje, że hello maszyny wirtualnej jest całkowicie usunięte z hello funkcji hypervisor, ale nadal dostępne w płaszczyźnie kontroli hello. Maszyny wirtualne w stanie Deallocated hello nie naliczenie opłat za obliczenia. |
| - | Wskazuje, że stan zasilania hello hello maszyny wirtualnej jest nieznany. |

### <a name="find-power-state"></a>Znajdź stan zasilania

Stan hello tooretrieve określonej maszyny wirtualnej, użyj hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) polecenia. Należy się toospecify poprawną nazwę maszyny wirtualnej i grupy zasobów. 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

Dane wyjściowe:

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a>Zadania zarządzania

Podczas cyklu życia hello maszyny wirtualnej może być toorun zadań zarządzania, takich jak uruchamianie, zatrzymywanie lub usuwanie maszyny wirtualnej. Ponadto można toocreate skrypty tooautomate powtarzających się lub złożonych zadań. Przy użyciu programu Azure PowerShell, wiele typowych zadań zarządzania można uruchomić z wiersza polecenia hello lub w skryptach.

### <a name="stop-virtual-machine"></a>Zatrzymaj maszynę wirtualną

Zatrzymaj i cofnięcia przydzielenia maszynie wirtualnej z [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

Jeśli chcesz maszyny wirtualnej hello tookeep w nim udostępnione, użyj parametru - StayProvisioned hello.

### <a name="start-virtual-machine"></a>Uruchom maszynę wirtualną

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a>Usuń grupę zasobów

Usunięcie grupy zasobów powoduje usunięcie wszystkie zasoby zawarte w ciągu.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a>Następne kroki

W tym samouczku poznanie podstawowych tworzenia maszyny Wirtualnej i zarządzania, np.:

> [!div class="checklist"]
> * Tworzenie i łączenie tooa maszyny Wirtualnej
> * Wybierz i używać obrazów maszyn wirtualnych
> * Wyświetlanie i używanie określonych rozmiarów maszyn wirtualnych
> * Zmienianie rozmiaru maszyny wirtualnej
> * Wyświetlanie i zrozumienie stanu maszyny Wirtualnej

Przejdź dalej toolearn samouczka toohello dysków maszyny Wirtualnej.  

> [!div class="nextstepaction"]
> [Utwórz i Zarządzaj maszyny Wirtualnej dyski](./tutorial-manage-data-disk.md)
