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
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a><span data-ttu-id="694f0-103">Konwertuj maszynę wirtualną systemu Windows z dysków toomanaged niezarządzane dysków</span><span class="sxs-lookup"><span data-stu-id="694f0-103">Convert a Windows virtual machine from unmanaged disks toomanaged disks</span></span>

<span data-ttu-id="694f0-104">Jeśli masz istniejące Windows maszynach wirtualnych (VM) korzystające z niezarządzanego dysków, można konwertować dyski toouse zarządzanych maszyn wirtualnych hello za pośrednictwem hello [dysków zarządzanych Azure](managed-disks-overview.md) usługi.</span><span class="sxs-lookup"><span data-stu-id="694f0-104">If you have existing Windows virtual machines (VMs) that use unmanaged disks, you can convert hello VMs toouse managed disks through hello [Azure Managed Disks](managed-disks-overview.md) service.</span></span> <span data-ttu-id="694f0-105">Ten proces konwersji dyskach hello systemu operacyjnego i wszystkich dysków dołączonych danych.</span><span class="sxs-lookup"><span data-stu-id="694f0-105">This process converts both hello OS disk and any attached data disks.</span></span>

<span data-ttu-id="694f0-106">W tym artykule opisano sposób tooconvert maszyn wirtualnych przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="694f0-106">This article shows you how tooconvert VMs by using Azure PowerShell.</span></span> <span data-ttu-id="694f0-107">Jeśli konieczne tooinstall lub uaktualnić go, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="694f0-107">If you need tooinstall or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="694f0-108">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="694f0-108">Before you begin</span></span>


* <span data-ttu-id="694f0-109">Przegląd [planowanie migracji hello dysków tooManaged](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span><span class="sxs-lookup"><span data-stu-id="694f0-109">Review [Plan for hello migration tooManaged Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a><span data-ttu-id="694f0-110">Konwertuj maszyn wirtualnych z jednego wystąpienia</span><span class="sxs-lookup"><span data-stu-id="694f0-110">Convert single-instance VMs</span></span>
<span data-ttu-id="694f0-111">W tej sekcji omówiono sposób tooconvert jednym wystąpieniu maszyny wirtualne platformy Azure z niezarządzanych dyski toomanaged dyski.</span><span class="sxs-lookup"><span data-stu-id="694f0-111">This section covers how tooconvert single-instance Azure VMs from unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="694f0-112">(W przypadku maszyn wirtualnych w zestawie dostępności, zobacz następną sekcję hello).</span><span class="sxs-lookup"><span data-stu-id="694f0-112">(If your VMs are in an availability set, see hello next section.)</span></span> 

1. <span data-ttu-id="694f0-113">Cofnięcie przydziału hello maszyny Wirtualnej za pomocą hello [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="694f0-113">Deallocate hello VM by using hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet.</span></span> <span data-ttu-id="694f0-114">Witaj poniższy przykład cofa alokację hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="694f0-114">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span> 

  ```powershell
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. <span data-ttu-id="694f0-115">Skonwertuj dyski toomanaged wirtualna hello przy użyciu hello [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="694f0-115">Convert hello VM toomanaged disks by using hello [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet.</span></span> <span data-ttu-id="694f0-116">Hello następującego procesu konwertuje hello poprzedniej maszyny Wirtualnej, w tym dysku hello systemu operacyjnego i dysków z danymi:</span><span class="sxs-lookup"><span data-stu-id="694f0-116">hello following process converts hello previous VM, including hello OS disk and any data disks:</span></span>

  ```powershell
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```

3. <span data-ttu-id="694f0-117">Rozpocznij hello maszyny Wirtualnej po hello konwersji toomanaged dysków za pomocą [Start AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="694f0-117">Start hello VM after hello conversion toomanaged disks by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm).</span></span> <span data-ttu-id="694f0-118">Po uruchomieniu przykład Hello hello poprzedniej maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="694f0-118">hello following example restarts hello previous VM:</span></span>

  ```powershell
  Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  ```


## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="694f0-119">Konwertuj maszyn wirtualnych w zestawie dostępności</span><span class="sxs-lookup"><span data-stu-id="694f0-119">Convert VMs in an availability set</span></span>

<span data-ttu-id="694f0-120">Hello maszyn wirtualnych, które mają tooconvert toomanaged dyski znajdują się w zestawie dostępności, należy najpierw tooconvert hello dostępność zestawu tooa zarządzanego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="694f0-120">If hello VMs that you want tooconvert toomanaged disks are in an availability set, you first need tooconvert hello availability set tooa managed availability set.</span></span>

1. <span data-ttu-id="694f0-121">Konwertuj dostępności hello skonfigurowane przy użyciu hello [AzureRmAvailabilitySet aktualizacji](/powershell/module/azurerm.compute/update-azurermavailabilityset) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="694f0-121">Convert hello availability set by using hello [Update-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet.</span></span> <span data-ttu-id="694f0-122">Poniższy przykład aktualizacji hello zestaw o nazwie dostępności Hello `myAvailabilitySet` hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="694f0-122">hello following example updates hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

  ```powershell
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  <span data-ttu-id="694f0-123">Jeśli region hello, gdzie znajduje się zestaw dostępności zawiera tylko 2 domen błędów zarządzanych, ale hello liczba domen błędów niezarządzane 3, to polecenie przedstawia błąd podobny zbyt "hello określona liczba domen błędów 3 musi należeć hello too2 zakresu 1."</span><span class="sxs-lookup"><span data-stu-id="694f0-123">If hello region where your availability set is located has only 2 managed fault domains but hello number of unmanaged fault domains is 3, this command shows an error similar too"hello specified fault domain count 3 must fall in hello range 1 too2."</span></span> <span data-ttu-id="694f0-124">Witaj tooresolve błąd, too2 domeny błędów hello aktualizacji i aktualizacji `Sku` zbyt`Aligned` w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="694f0-124">tooresolve hello error, update hello fault domain too2 and update `Sku` too`Aligned` as follows:</span></span>

  ```powershell
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. <span data-ttu-id="694f0-125">Cofnięcie przydziału i przekonwertować maszyny wirtualne hello w zestawie dostępności hello.</span><span class="sxs-lookup"><span data-stu-id="694f0-125">Deallocate and convert hello VMs in hello availability set.</span></span> <span data-ttu-id="694f0-126">Hello poniższy skrypt cofa alokację każdej maszyny Wirtualnej za pomocą hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) konwertuje go za pomocą polecenia cmdlet, [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk)i ponownie go uruchamia przy użyciu [Start AzureRmVM ](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="694f0-126">hello following script deallocates each VM by using hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet, converts it by using [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk), and restarts it by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

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


## <a name="troubleshooting"></a><span data-ttu-id="694f0-127">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="694f0-127">Troubleshooting</span></span>

<span data-ttu-id="694f0-128">Jeśli występuje błąd podczas konwersji lub Jeśli maszyna wirtualna jest w stanie awarii z powodu problemów dotyczących w poprzedniej konwersji, uruchom hello `ConvertTo-AzureRmVMManagedDisk` ponownie polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="694f0-128">If there is an error during conversion, or if a VM is in a failed state because of issues in a previous conversion, run hello `ConvertTo-AzureRmVMManagedDisk` cmdlet again.</span></span> <span data-ttu-id="694f0-129">Proste ponownych prób zwykle odblokowuje hello sytuacji.</span><span class="sxs-lookup"><span data-stu-id="694f0-129">A simple retry usually unblocks hello situation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="694f0-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="694f0-130">Next steps</span></span>

[<span data-ttu-id="694f0-131">Konwertuj toopremium dyski standardowe zarządzanych</span><span class="sxs-lookup"><span data-stu-id="694f0-131">Convert standard managed disks toopremium</span></span>](convert-disk-storage.md)

<span data-ttu-id="694f0-132">Podjąć tylko do odczytu kopię maszyny Wirtualnej za pomocą [migawki](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="694f0-132">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

