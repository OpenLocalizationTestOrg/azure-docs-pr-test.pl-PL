---
title: "aaaConvert maszynę wirtualną systemu Windows z niezarządzanych dyski dysków toomanaged - dysków zarządzanych Azure | Dokumentacja firmy Microsoft"
description: "Jak tooconvert maszyny Wirtualnej systemu Windows z dysków niezarządzane toomanaged dyski za pomocą programu PowerShell w modelu wdrażania usługi Resource Manager hello"
services: virtual-machines-windows
documentationcenter: 
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
ms.date: 06/23/2017
ms.author: cynthn
ms.openlocfilehash: e8ed8694b0e776d22df26261e2fc8340bfe5cafa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a>Konwertuj maszynę wirtualną systemu Windows z dysków toomanaged niezarządzane dysków

Jeśli masz istniejące Windows maszynach wirtualnych (VM) korzystające z niezarządzanego dysków, można konwertować dyski toouse zarządzanych maszyn wirtualnych hello za pośrednictwem hello [dysków zarządzanych Azure](managed-disks-overview.md) usługi. Ten proces konwersji dyskach hello systemu operacyjnego i wszystkich dysków dołączonych danych.

W tym artykule opisano sposób tooconvert maszyn wirtualnych przy użyciu programu Azure PowerShell. Jeśli konieczne tooinstall lub uaktualnić go, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/install-azurerm-ps.md).

## <a name="before-you-begin"></a>Przed rozpoczęciem


* Przegląd [planowanie migracji hello dysków tooManaged](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a>Konwertuj maszyn wirtualnych z jednego wystąpienia
W tej sekcji omówiono sposób tooconvert jednym wystąpieniu maszyny wirtualne platformy Azure z niezarządzanych dyski toomanaged dyski. (W przypadku maszyn wirtualnych w zestawie dostępności, zobacz następną sekcję hello). 

1. Cofnięcie przydziału hello maszyny Wirtualnej za pomocą hello [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) polecenia cmdlet. Witaj poniższy przykład cofa alokację hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`: 

  ```powershell
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. Skonwertuj dyski toomanaged wirtualna hello przy użyciu hello [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) polecenia cmdlet. Hello następującego procesu konwertuje hello poprzedniej maszyny Wirtualnej, w tym dysku hello systemu operacyjnego i dysków z danymi:

  ```powershell
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```

3. Rozpocznij hello maszyny Wirtualnej po hello konwersji toomanaged dysków za pomocą [Start AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm). Po uruchomieniu przykład Hello hello poprzedniej maszyny Wirtualnej:

  ```powershell
  Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  ```


## <a name="convert-vms-in-an-availability-set"></a>Konwertuj maszyn wirtualnych w zestawie dostępności

Hello maszyn wirtualnych, które mają tooconvert toomanaged dyski znajdują się w zestawie dostępności, należy najpierw tooconvert hello dostępność zestawu tooa zarządzanego zestawu dostępności.

1. Konwertuj dostępności hello skonfigurowane przy użyciu hello [AzureRmAvailabilitySet aktualizacji](/powershell/module/azurerm.compute/update-azurermavailabilityset) polecenia cmdlet. Poniższy przykład aktualizacji hello zestaw o nazwie dostępności Hello `myAvailabilitySet` hello grupy zasobów o nazwie `myResourceGroup`:

  ```powershell
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  Jeśli region hello, gdzie znajduje się zestaw dostępności zawiera tylko 2 domen błędów zarządzanych, ale hello liczba domen błędów niezarządzane 3, to polecenie przedstawia błąd podobny zbyt "hello określona liczba domen błędów 3 musi należeć hello too2 zakresu 1." Witaj tooresolve błąd, too2 domeny błędów hello aktualizacji i aktualizacji `Sku` zbyt`Aligned` w następujący sposób:

  ```powershell
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. Cofnięcie przydziału i przekonwertować maszyny wirtualne hello w zestawie dostępności hello. Hello poniższy skrypt cofa alokację każdej maszyny Wirtualnej za pomocą hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) konwertuje go za pomocą polecenia cmdlet, [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk)i ponownie go uruchamia przy użyciu [Start AzureRmVM ](/powershell/module/azurerm.compute/start-azurermvm):

  ```powershell
  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName

  foreach($vmInfo in $avSet.VirtualMachinesReferences)
  {
     $vm = Get-AzureRmVM -ResourceGroupName $rgName | Where-Object {$_.Id -eq $vmInfo.id}
     Stop-AzureRmVM -ResourceGroupName $rgName -Name $vm.Name -Force
     ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vm.Name
     Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  }
  ```


## <a name="troubleshooting"></a>Rozwiązywanie problemów

Jeśli występuje błąd podczas konwersji lub Jeśli maszyna wirtualna jest w stanie awarii z powodu problemów dotyczących w poprzedniej konwersji, uruchom hello `ConvertTo-AzureRmVMManagedDisk` ponownie polecenia cmdlet. Proste ponownych prób zwykle odblokowuje hello sytuacji.


## <a name="next-steps"></a>Następne kroki

[Konwertuj toopremium dyski standardowe zarządzanych](convert-disk-storage.md)

Podjąć tylko do odczytu kopię maszyny Wirtualnej za pomocą [migawki](snapshot-copy-managed-disk.md).

