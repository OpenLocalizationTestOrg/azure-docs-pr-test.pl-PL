---
title: "Samouczek zestawy dostępności dla maszyn wirtualnych systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: "Informacje na temat zestawów dostępności dla maszyn wirtualnych systemu Windows na platformie Azure."
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
ms.openlocfilehash: d918362106ef93cf47620e0018d363cd510884b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-availability-sets"></a>Jak używać zestawów dostępności

Z tego samouczka dowiesz się, jak zwiększyć dostępność i niezawodność rozwiązań maszyny wirtualnej na platformie Azure przy użyciu funkcji o nazwie zestawów dostępności. Zestawy dostępności upewnij się, czy maszyn wirtualnych, należy wdrożyć na platformie Azure są rozproszone na wielu klastrów izolowanego sprzętu. W ten sposób zapewnia, że jeśli awarii sprzętu lub oprogramowania w systemie Azure wykonywany, jest ograniczona tylko do podzbioru maszyny wirtualne i które rozwiązania ogólną pozostanie dostępny i działa z perspektywy klientów przy użyciu go. 

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tworzenie zestawu dostępności
> * Tworzenie maszyny Wirtualnej w zestawie dostępności
> * Sprawdź dostępne rozmiary maszyny Wirtualnej

Dla tego samouczka jest wymagany moduł Azure PowerShell w wersji 3.6 lub nowszej. Uruchom polecenie ` Get-Module -ListAvailable AzureRM`, aby dowiedzieć się, jaka wersja jest używana. Jeśli potrzebujesz do uaktualnienia, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="availability-set-overview"></a>Omówienie zestawu dostępności

Zestawu dostępności jest możliwość grupę logiczną, która na platformie Azure umożliwia Sprawdź, czy zasobów maszyny Wirtualnej, który można umieścić w nim są odizolowane od siebie, gdy są wdrożone w centrum danych Azure. Azure zapewnia, że maszyny wirtualne, umieść w ramach zestawu dostępności uruchamiania na wielu serwerach fizycznych, obliczeniowe stojakami jednostek magazynowych i przełączniki sieciowe. Dzięki temu w przypadku awarii sprzętu lub oprogramowania Azure awarii, jest ograniczona tylko podzestaw maszyn wirtualnych, a aplikacja ogólna pozostanie w górę i nadal dostępne dla klientów. Przy użyciu zestawów dostępności jest podstawowych możliwości wykorzystać umożliwia tworzenia rozwiązań chmur wiarygodne.

Zastanówmy typowe rozwiązania oparte na Maszynach którym może mieć 4 serwery frontonu sieci web i korzystać z 2 maszyny wirtualne zaplecza, które hostują bazy danych. Przy użyciu platformy Azure, należy zdefiniować dwa zestawy dostępności, przed wdrożeniem maszyn wirtualnych: jeden zbiór dostępności dla warstwy "web" i jeden zbiór dostępności dla warstwy "baza danych". Podczas tworzenia nowej maszyny Wirtualnej można określić zestaw dostępności jako parametr do maszyny wirtualnej az utworzyć polecenie, a Azure zostanie automatycznie upewnij się, że maszyny wirtualne utworzone w zestawie dostępne są izolowane między wieloma zasobami sprzętu fizycznego. Oznacza to, że jeśli sprzęt fizyczny wykorzystywany do jednego serwera sieci Web lub maszyn wirtualnych z serwera bazy danych jest uruchomiona na ma problem, wiesz, że inne wystąpienia serwera sieci Web i bazy danych w maszynach wirtualnych pozostaną uruchomione prawidłowo ponieważ są one na inny komputer.

Zawsze należy używać zestawów dostępności, jeśli chcesz wdrożyć niezawodne rozwiązania na podstawie maszyny Wirtualnej w obrębie platformy Azure.

## <a name="create-an-availability-set"></a>Tworzenie zestawu dostępności

Możesz utworzyć zestaw przy użyciu danych o dostępności [AzureRmAvailabilitySet nowy](/powershell/module/azurerm.compute/new-azurermavailabilityset). W tym przykładzie umieszczania liczba domen aktualizacji i odporność na *2* dla zestawu o nazwie dostępności *myAvailabilitySet* w *myResourceGroupAvailability* grupy zasobów.

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

Maszyny wirtualne muszą można utworzyć dostępność ustawioną upewnij się, że są one poprawnie dystrybuowana sprzętu. Nie można dodać istniejącej maszyny Wirtualnej do dostępności po jego utworzeniu. 

Sprzęt w lokalizacji jest podzielony na wiele domen aktualizacji i domen błędów. **Domeny aktualizacji** jest grupą maszyn wirtualnych i podstawowym sprzętem fizycznym, który może zostać uruchomiony ponownie w tym samym czasie. Maszyny wirtualne w tej samej **domeny błędów** udostępnianie typowych magazynu, a także wspólnego przełącznik źródła i sieci zasilania. 

Po utworzeniu maszyny Wirtualnej przy użyciu konfiguracji przy użyciu [AzureRMVMConfig nowy](/powershell/module/azurerm.compute/new-azurermvmconfig) określ zestaw, za pomocą dostępności `-AvailabilitySetId` parametr, aby określić identyfikator zestawu dostępności.

Tworzenie 2 maszyn wirtualnych z [AzureRmVM nowy](/powershell/module/azurerm.compute/new-azurermvm) w zestawie dostępności.

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for the virtual machine."

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

   # Here is where we specify the availability set
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

Trwa kilka minut, aby utworzyć i skonfigurować obie maszyny wirtualne. Po zakończeniu będziesz mieć 2 maszyny wirtualne rozproszone na używanego sprzętu. 

## <a name="check-for-available-vm-sizes"></a>Sprawdź, czy dostępne rozmiary maszyny Wirtualnej 

Możesz dodać więcej maszyn wirtualnych do później zestaw dostępności, ale musisz wiedzieć, jaki rozmiarów maszyn wirtualnych są dostępne na sprzęcie. Użyj [Get AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) Aby wyświetlić listę wszystkich dostępnych rozmiarów na sprzęcie klastra dla zestawu dostępności.

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

Przejdź do następnego samouczkiem, aby poznać zestawy skalowania maszyny wirtualnej.

> [!div class="nextstepaction"]
> [Tworzenie zestawu skalowania maszyn wirtualnych](tutorial-create-vmss.md)


