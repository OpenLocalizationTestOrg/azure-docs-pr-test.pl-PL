---
title: aaaAvailability ustawia samouczek dla maszyn wirtualnych systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat hello dostępności zestawów dla maszyn wirtualnych systemu Windows na platformie Azure."
documentationcenter: 
services: virtual-machines-windows
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 853775c5f126dd815c1933f9d71d2274a75ea661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a>Jak zestawy dostępności toouse

Z tego samouczka dowiesz się, jak tooincrease hello dostępność i niezawodność rozwiązań maszyny wirtualnej na platformie Azure przy użyciu funkcji o nazwie zestawów dostępności. Zestawy dostępności upewnij się, tym powitalne wdrażanie na platformie Azure maszyny wirtualne rozproszone na wielu klastrów izolowanego sprzętu. W ten sposób zapewnia, że jeśli awarii sprzętu lub oprogramowania w systemie Azure wykonywany, jest ograniczona tylko do podzbioru maszyny wirtualne i które rozwiązania ogólną pozostanie dostępny i działa z punktu widzenia hello klientów przy użyciu go. 

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tworzenie zestawu dostępności
> * Tworzenie maszyny Wirtualnej w zestawie dostępności
> * Sprawdź dostępne rozmiary maszyny Wirtualnej

Ten samouczek wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej. Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji. Jeśli potrzebujesz tooupgrade, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="availability-set-overview"></a>Omówienie zestawu dostępności

Zestawu dostępności jest funkcją logicznego grupowania, które można użyć w Azure tooensure hello zasobów maszyny Wirtualnej, który można umieścić w niej są odizolowane od siebie, gdy są wdrożone w centrum danych Azure. Azure zapewnia, że hello maszyn wirtualnych zostanie umieszczony w obrębie zestawu dostępności uruchamiania na wielu serwerach fizycznych, obliczeniowe stojakami jednostek magazynowych i przełączniki sieciowe. Dzięki temu w zdarzeniu hello sprzętu lub oprogramowania Azure awarii, jest ograniczona tylko podzestaw maszyn wirtualnych, a pozostanie się i kontynuować klientów dostępne tooyour toobe ogólną aplikacji. Przy użyciu zestawów dostępności jest tooleverage podstawowych możliwości, gdy trzeba toobuild niezawodne rozwiązania.

Zastanówmy typowe rozwiązania oparte na Maszynach którym może mieć 4 serwery frontonu sieci web i korzystać z 2 maszyny wirtualne zaplecza, które hostują bazy danych. Przy użyciu platformy Azure, trzeba będzie toodefine dwa zestawy dostępności przed wdrożeniem maszyny wirtualne: zbiór jednej dostępności dla warstwy "web" hello i jeden zbiór dostępności dla warstwy "baza danych" hello. Podczas tworzenia nowej maszyny Wirtualnej można określić zestaw jako maszynę wirtualną az toohello parametr Utwórz polecenie, a Azure zostanie automatycznie upewnij się, że hello maszyny wirtualne utworzone w hello dostępne dostępności hello zestawu są izolowane między wieloma zasobami sprzętu fizycznego. Oznacza to, że jeśli hello sprzętem fizycznym, który działa jeden z serwera sieci Web lub maszyn wirtualnych z serwera bazy danych na ma problem, wiesz, że hello inne wystąpienia serwera sieci Web i bazy danych w maszynach wirtualnych pozostanie uruchomione prawidłowo, ponieważ znajdują się na inny komputer.

Zawsze należy używać zestawów dostępności, jeśli chcesz toodeploy niezawodne rozwiązania na podstawie maszyny Wirtualnej w obrębie platformy Azure.

## <a name="create-an-availability-set"></a>Tworzenie zestawu dostępności

Możesz utworzyć zestaw przy użyciu danych o dostępności [AzureRmAvailabilitySet nowy](/powershell/module/azurerm.compute/new-azurermavailabilityset). W tym przykładzie ustawiliśmy na obu hello liczby domen aktualizacji i odporność na *2* dla zestawu o nazwie dostępności hello *myAvailabilitySet* w hello *myResourceGroupAvailability*grupy zasobów.

Utwórz grupę zasobów.

```powershell
New-AzureRmResourceGroup -Name myResourceGroupAvailability -Location EastUS
```


```powershell
New-AzureRmAvailabilitySet `
   -Location EastUS `
   -Name myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability `
   -Managed `
   -PlatformFaultDomainCount 2 `
   -PlatformUpdateDomainCount 2
```

## <a name="create-vms-inside-an-availability-set"></a>Tworzenie maszyn wirtualnych w zestawie dostępności

Maszyny wirtualne muszą toobe utworzone w ramach toomake zestaw dostępności hello się, że poprawnie dystrybuowana ich hello sprzętu. Nie można dodać istniejącej maszyny Wirtualnej tooan zestaw danych o dostępności po jego utworzeniu. 

sprzętu Hello w lokalizacji jest podzielony na domeny aktualizacji toomultiple i domen błędów. **Domeny aktualizacji** grupy maszyn wirtualnych i podstawowym sprzętem fizycznym, który może zostać przeprowadzony ponowny rozruch w hello jest tym samym czasie. Maszyny wirtualne w hello sam **domeny błędów** udostępnianie typowych magazynu, a także wspólnego przełącznik źródła i sieci zasilania. 

Po utworzeniu maszyny Wirtualnej przy użyciu konfiguracji przy użyciu [AzureRMVMConfig nowy](/powershell/module/azurerm.compute/new-azurermvmconfig) Określ dostępności hello ustawić za pomocą hello `-AvailabilitySetId` identyfikator hello toospecify parametru hello zestawu dostępności.

Tworzenie 2 maszyn wirtualnych z [AzureRmVM nowy](/powershell/module/azurerm.compute/new-azurermvm) w zestawie dostępności hello.

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAvailability `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

for ($i=1; $i -le 2; $i++)
{
   $pip = New-AzureRmPublicIpAddress `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name "mypublicdns$(Get-Random)" `
        -AllocationMethod Static `
        -IdleTimeoutInMinutes 4

   $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
        -Name myNetworkSecurityGroupRuleRDP$i `
        -Protocol Tcp `
        -Direction Inbound `
        -Priority 1000 `
        -SourceAddressPrefix * `
        -SourcePortRange * `
        -DestinationAddressPrefix * `
        -DestinationPortRange 3389 `
        -Access Allow

   $nsg = New-AzureRmNetworkSecurityGroup `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name myNetworkSecurityGroup$i `
        -SecurityRules $nsgRuleRDP

   $nic = New-AzureRmNetworkInterface `
        -Name myNic$i `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -SubnetId $vnet.Subnets[0].Id `
        -PublicIpAddressId $pip.Id `
        -NetworkSecurityGroupId $nsg.Id

   # Here is where we specify hello availability set
   $vm = New-AzureRmVMConfig `
        -VMName myVM$i `
        -VMSize Standard_D1 `
        -AvailabilitySetId $availabilitySet.Id

   $vm = Set-AzureRmVMOperatingSystem `
        -VM $vm `
        -Windows -ComputerName myVM$i `   
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
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -VM $vm
}

```

Go zajmuje kilka minut toocreate i skonfiguruj obie maszyny wirtualne. Po zakończeniu będziesz mieć 2 maszyny wirtualne rozproszone na powitania podstawowy sprzęt. 

## <a name="check-for-available-vm-sizes"></a>Sprawdź, czy dostępne rozmiary maszyny Wirtualnej 

Możesz dodać więcej maszyn wirtualnych później zestaw dostępności toohello, ale trzeba się tooknow rozmiarów maszyn wirtualnych, które są dostępne na powitania sprzętu. Użyj [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist wszystkie dostępne rozmiary hello na powitania sprzętu klastra hello zestawu dostępności.

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a>Następne kroki

W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tworzenie zestawu dostępności
> * Tworzenie maszyny Wirtualnej w zestawie dostępności
> * Sprawdź dostępne rozmiary maszyny Wirtualnej

Przejdź dalej toolearn samouczka toohello o zestawy skalowania maszyny wirtualnej.

> [!div class="nextstepaction"]
> [Tworzenie zestawu skalowania maszyn wirtualnych](tutorial-create-vmss.md)


