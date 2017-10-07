---
title: aaaUse PowerShell tooresize maszyny Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Zmień rozmiar maszyny wirtualnej systemu Windows, utworzony w modelu wdrażania usługi Resource Manager hello przy użyciu programu Azure Powershell."
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 057ff274-6dad-415e-891c-58f8eea9ed78
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: a4a80f3bc99911e4f1a095f0ce63aca00fa50694
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm"></a>Zmień rozmiar maszyny Wirtualnej systemu Windows
W tym artykule opisano, jak tooresize maszyny Wirtualnej systemu Windows, utworzonej w modelu wdrażania usługi Resource Manager hello przy użyciu programu Azure Powershell.

Po utworzeniu maszyny wirtualnej (VM), można skalować hello maszyny Wirtualnej w górę lub w dół, zmieniając hello rozmiar maszyny Wirtualnej. W niektórych przypadkach należy najpierw cofnąć hello maszyny Wirtualnej. Może to nastąpić, jeśli hello nowy rozmiar jest niedostępny na powitania sprzętu klastra, które obecnie obsługuje hello maszyny Wirtualnej.

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a>Zmień rozmiar maszyny Wirtualnej systemu Windows, nie znajduje się w zbiorze dostępności
1. Wyświetl listę hello rozmiarów maszyn wirtualnych, które są dostępne na powitania sprzętu klastra, gdzie jest hostowana hello maszyny Wirtualnej. 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. W razie potrzeby hello znajduje się rozmiar Uruchom hello następujące polecenia tooresize hello maszyny Wirtualnej. W razie potrzeby hello się, że nie ma rozmiar Przejdź toostep 3.
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. W razie potrzeby hello się, że nie ma rozmiar Uruchom hello następujące polecenia toodeallocate hello maszyny Wirtualnej, rozmiar i ponownie uruchom hello maszyny Wirtualnej.
   
    ```powershell
    $rgname = "<resourceGroupName>"
    $vmname = "<vmName>"
    Stop-AzureRmVM -ResourceGroupName $rgname -VMName $vmname -Force
    $vm = Get-AzureRmVM -ResourceGroupName $rgname -VMName $vmname
    $vm.HardwareProfile.VmSize = "<newVMSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName $rgname
    Start-AzureRmVM -ResourceGroupName $rgname -Name $vmname
    ```

> [!WARNING]
> Cofanie przydziału hello wirtualna zwalnia dynamiczne adresy IP przypisane toohello maszyny Wirtualnej. nie dotyczy Hello systemu operacyjnego i dysków z danymi. 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a>Zmień rozmiar maszyny Wirtualnej systemu Windows w zestawie dostępności
Jeśli hello nowy rozmiar maszyny Wirtualnej w zestawie dostępności nie jest dostępne w klastrze sprzętu hello aktualnie obsługujący hello maszyny Wirtualnej, a następnie wszystkich maszyn wirtualnych w zestawie dostępności hello należy toobe alokację hello tooresize maszyny Wirtualnej. Należy również tooupdate hello rozmiar innych maszyn wirtualnych w dostępności powitania po jednej maszyny Wirtualnej został zmieniony. tooresize maszyny Wirtualnej w zestawie dostępności, wykonaj hello następujące kroki.

1. Wyświetl listę hello rozmiarów maszyn wirtualnych, które są dostępne na powitania sprzętu klastra, gdzie jest hostowana hello maszyny Wirtualnej.
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. W razie potrzeby hello znajduje się rozmiar Uruchom hello następujące polecenia tooresize hello maszyny Wirtualnej. Jeśli nie ma na liście, przejdź toostep 3.
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. W razie potrzeby hello się, że nie ma rozmiar kontynuować hello następujące kroki toodeallocate wszystkich maszyn wirtualnych w zestawie dostępności hello, Zmień rozmiar maszyn wirtualnych i uruchomić je ponownie.
4. Zatrzymanie wszystkich maszyn wirtualnych w zestawie dostępności hello.
   
   ```powershell
   $rg = "<resourceGroupName>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     Stop-AzureRmVM -ResourceGroupName $rg -Name $vmName -Force
   } 
   ```
5. Zmień rozmiar i ponownie uruchom hello maszyn wirtualnych w zestawie dostępności hello.
   
   ```powershell
   $rg = "<resourceGroupName>"
   $newSize = "<newVmSize>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     $vm = Get-AzureRmVM -ResourceGroupName $rg -Name $vmName
     $vm.HardwareProfile.VmSize = $newSize
     Update-AzureRmVM -ResourceGroupName $rg -VM $vm
     Start-AzureRmVM -ResourceGroupName $rg -Name $vmName
   }
   ```

## <a name="next-steps"></a>Następne kroki
* Dodatkowe możliwości skalowania uruchamianie wielu wystąpień maszyny Wirtualnej i skalowanie w poziomie. Aby uzyskać więcej informacji, zobacz [automatycznie skalować w zestawie skalowania maszyn wirtualnych systemu Windows maszyny](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).

