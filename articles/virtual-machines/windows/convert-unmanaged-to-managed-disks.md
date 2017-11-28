---
title: "Konwertuj maszyny wirtualnej systemu Windows z dysków niezarządzanych do zarządzanych dysków - Azure zarządzanych dysków | Dokumentacja firmy Microsoft"
description: "Sposób konwertowania maszyny Wirtualnej systemu Windows z dysków niezarządzanych do zarządzanych dysków za pomocą programu PowerShell w modelu wdrażania usługi Resource Manager"
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
ms.openlocfilehash: 54afcf1e37f696979bfe270a473c72aedf20dc43
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-to-managed-disks"></a><span data-ttu-id="fb8ac-103">Konwertuj maszynę wirtualną systemu Windows z dysków niezarządzanych do zarządzanych dysków</span><span class="sxs-lookup"><span data-stu-id="fb8ac-103">Convert a Windows virtual machine from unmanaged disks to managed disks</span></span>

<span data-ttu-id="fb8ac-104">Jeśli masz istniejące Windows maszynach wirtualnych (VM) korzystające z niezarządzanego dysków, można przekonwertować maszyny wirtualne do zarządzanych dysków za pomocą [dysków zarządzanych Azure](managed-disks-overview.md) usługi.</span><span class="sxs-lookup"><span data-stu-id="fb8ac-104">If you have existing Windows virtual machines (VMs) that use unmanaged disks, you can convert the VMs to use managed disks through the [Azure Managed Disks](managed-disks-overview.md) service.</span></span> <span data-ttu-id="fb8ac-105">Ten proces konwersji zarówno dysk systemu operacyjnego i wszystkich dysków dołączonych danych.</span><span class="sxs-lookup"><span data-stu-id="fb8ac-105">This process converts both the OS disk and any attached data disks.</span></span>

<span data-ttu-id="fb8ac-106">W tym artykule przedstawiono sposób konwertowania maszyn wirtualnych przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fb8ac-106">This article shows you how to convert VMs by using Azure PowerShell.</span></span> <span data-ttu-id="fb8ac-107">Jeśli musisz zainstalować lub uaktualnić go, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="fb8ac-107">If you need to install or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fb8ac-108">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="fb8ac-108">Before you begin</span></span>


* <span data-ttu-id="fb8ac-109">Przegląd [planowanie migracji do zarządzanych dysków](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span><span class="sxs-lookup"><span data-stu-id="fb8ac-109">Review [Plan for the migration to Managed Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a><span data-ttu-id="fb8ac-110">Konwertuj maszyn wirtualnych z jednego wystąpienia</span><span class="sxs-lookup"><span data-stu-id="fb8ac-110">Convert single-instance VMs</span></span>
<span data-ttu-id="fb8ac-111">W tej sekcji omówiono sposób konwertowania maszyn wirtualnych Azure jednym wystąpieniu z dysków niezarządzanych do zarządzanych dysków.</span><span class="sxs-lookup"><span data-stu-id="fb8ac-111">This section covers how to convert single-instance Azure VMs from unmanaged disks to managed disks.</span></span> <span data-ttu-id="fb8ac-112">(W przypadku maszyn wirtualnych w zestawie dostępności, zobacz następną sekcję).</span><span class="sxs-lookup"><span data-stu-id="fb8ac-112">(If your VMs are in an availability set, see the next section.)</span></span> 

1. <span data-ttu-id="fb8ac-113">Cofnięcie przydziału maszyny Wirtualnej za pomocą [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fb8ac-113">Deallocate the VM by using the [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet.</span></span> <span data-ttu-id="fb8ac-114">Poniższy przykład cofa alokację maszyny Wirtualnej o nazwie `myVM` w grupie zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="fb8ac-114">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span></span> 

  ```powershell
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. <span data-ttu-id="fb8ac-115">Konwertuj maszynę Wirtualną do zarządzanych dysków za pomocą [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fb8ac-115">Convert the VM to managed disks by using the [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet.</span></span> <span data-ttu-id="fb8ac-116">Następujący proces konwertuje poprzedniej maszyny Wirtualnej, w tym dysku systemu operacyjnego i dysków z danymi:</span><span class="sxs-lookup"><span data-stu-id="fb8ac-116">The following process converts the previous VM, including the OS disk and any data disks:</span></span>

  ```powershell
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```

3. <span data-ttu-id="fb8ac-117">Uruchom maszynę Wirtualną po konwersji do dysków zarządzanych za pomocą [Start AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="fb8ac-117">Start the VM after the conversion to managed disks by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm).</span></span> <span data-ttu-id="fb8ac-118">Poniższy przykład ponowne uruchomienie poprzedniego maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="fb8ac-118">The following example restarts the previous VM:</span></span>

  ```powershell
  Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  ```


## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="fb8ac-119">Konwertuj maszyn wirtualnych w zestawie dostępności</span><span class="sxs-lookup"><span data-stu-id="fb8ac-119">Convert VMs in an availability set</span></span>

<span data-ttu-id="fb8ac-120">Jeśli maszyny wirtualne, które ma zostać przekonwertowany na zarządzany dyski znajdują się w zestawie dostępności, należy najpierw przekonwertować zestaw z zestawem dostępności zarządzanego dostępności.</span><span class="sxs-lookup"><span data-stu-id="fb8ac-120">If the VMs that you want to convert to managed disks are in an availability set, you first need to convert the availability set to a managed availability set.</span></span>

1. <span data-ttu-id="fb8ac-121">Konwertuj zestawu za pomocą dostępności [AzureRmAvailabilitySet aktualizacji](/powershell/module/azurerm.compute/update-azurermavailabilityset) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fb8ac-121">Convert the availability set by using the [Update-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet.</span></span> <span data-ttu-id="fb8ac-122">Poniższy przykład aktualizuje zestaw o nazwie dostępności `myAvailabilitySet` w grupie zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="fb8ac-122">The following example updates the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span></span>

  ```powershell
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  <span data-ttu-id="fb8ac-123">Jeśli znajduje się regionu, w których wartość jego dostępność ma tylko 2 domen błędów zarządzanych, ale liczba domen błędów niezarządzanym jest 3, to polecenie przedstawia błąd podobny do "określona liczba domen błędów 3 musi należeć do zakresu od 1 do 2."</span><span class="sxs-lookup"><span data-stu-id="fb8ac-123">If the region where your availability set is located has only 2 managed fault domains but the number of unmanaged fault domains is 3, this command shows an error similar to "The specified fault domain count 3 must fall in the range 1 to 2."</span></span> <span data-ttu-id="fb8ac-124">Aby rozwiązać problem, zaktualizuj domeny błędów 2 i aktualizacji `Sku` do `Aligned` w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="fb8ac-124">To resolve the error, update the fault domain to 2 and update `Sku` to `Aligned` as follows:</span></span>

  ```powershell
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. <span data-ttu-id="fb8ac-125">Cofnięcie przydziału i przekonwertować maszyny wirtualne w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="fb8ac-125">Deallocate and convert the VMs in the availability set.</span></span> <span data-ttu-id="fb8ac-126">Poniższy skrypt cofa alokację każdej maszyny Wirtualnej za pomocą [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) konwertuje go za pomocą polecenia cmdlet, [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk)i ponownie go uruchamia przy użyciu [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="fb8ac-126">The following script deallocates each VM by using the [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet, converts it by using [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk), and restarts it by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

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


## <a name="troubleshooting"></a><span data-ttu-id="fb8ac-127">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="fb8ac-127">Troubleshooting</span></span>

<span data-ttu-id="fb8ac-128">Jeśli występuje błąd podczas konwersji lub Jeśli maszyna wirtualna jest w stanie awarii z powodu problemów dotyczących w poprzedniej konwersji, uruchom `ConvertTo-AzureRmVMManagedDisk` ponownie polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fb8ac-128">If there is an error during conversion, or if a VM is in a failed state because of issues in a previous conversion, run the `ConvertTo-AzureRmVMManagedDisk` cmdlet again.</span></span> <span data-ttu-id="fb8ac-129">Proste ponownych prób zwykle odblokowuje sytuacji.</span><span class="sxs-lookup"><span data-stu-id="fb8ac-129">A simple retry usually unblocks the situation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fb8ac-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fb8ac-130">Next steps</span></span>

[<span data-ttu-id="fb8ac-131">Konwertuj dyski standardowe zarządzanego na — wersja premium</span><span class="sxs-lookup"><span data-stu-id="fb8ac-131">Convert standard managed disks to premium</span></span>](convert-disk-storage.md)

<span data-ttu-id="fb8ac-132">Podjąć tylko do odczytu kopię maszyny Wirtualnej za pomocą [migawki](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="fb8ac-132">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

