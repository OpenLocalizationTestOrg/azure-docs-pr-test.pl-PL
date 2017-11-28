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
# <a name="resize-a-windows-vm"></a><span data-ttu-id="4e1cf-103">Zmień rozmiar maszyny Wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="4e1cf-103">Resize a Windows VM</span></span>
<span data-ttu-id="4e1cf-104">W tym artykule opisano, jak tooresize maszyny Wirtualnej systemu Windows, utworzonej w modelu wdrażania usługi Resource Manager hello przy użyciu programu Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="4e1cf-104">This article shows you how tooresize a Windows VM, created in hello Resource Manager deployment model using Azure Powershell.</span></span>

<span data-ttu-id="4e1cf-105">Po utworzeniu maszyny wirtualnej (VM), można skalować hello maszyny Wirtualnej w górę lub w dół, zmieniając hello rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4e1cf-105">After you create a virtual machine (VM), you can scale hello VM up or down by changing hello VM size.</span></span> <span data-ttu-id="4e1cf-106">W niektórych przypadkach należy najpierw cofnąć hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4e1cf-106">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="4e1cf-107">Może to nastąpić, jeśli hello nowy rozmiar jest niedostępny na powitania sprzętu klastra, które obecnie obsługuje hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4e1cf-107">This can happen if hello new size is not available on hello hardware cluster that is currently hosting hello VM.</span></span>

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a><span data-ttu-id="4e1cf-108">Zmień rozmiar maszyny Wirtualnej systemu Windows, nie znajduje się w zbiorze dostępności</span><span class="sxs-lookup"><span data-stu-id="4e1cf-108">Resize a Windows VM not in an availability set</span></span>
1. <span data-ttu-id="4e1cf-109">Wyświetl listę hello rozmiarów maszyn wirtualnych, które są dostępne na powitania sprzętu klastra, gdzie jest hostowana hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4e1cf-109">List hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span> 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. <span data-ttu-id="4e1cf-110">W razie potrzeby hello znajduje się rozmiar Uruchom hello następujące polecenia tooresize hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4e1cf-110">If hello desired size is listed, run hello following commands tooresize hello VM.</span></span> <span data-ttu-id="4e1cf-111">W razie potrzeby hello się, że nie ma rozmiar Przejdź toostep 3.</span><span class="sxs-lookup"><span data-stu-id="4e1cf-111">If hello desired size is not listed, go on toostep 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="4e1cf-112">W razie potrzeby hello się, że nie ma rozmiar Uruchom hello następujące polecenia toodeallocate hello maszyny Wirtualnej, rozmiar i ponownie uruchom hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4e1cf-112">If hello desired size is not listed, run hello following commands toodeallocate hello VM, resize it, and restart hello VM.</span></span>
   
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
> <span data-ttu-id="4e1cf-113">Cofanie przydziału hello wirtualna zwalnia dynamiczne adresy IP przypisane toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4e1cf-113">Deallocating hello VM releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="4e1cf-114">nie dotyczy Hello systemu operacyjnego i dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="4e1cf-114">hello OS and data disks are not affected.</span></span> 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a><span data-ttu-id="4e1cf-115">Zmień rozmiar maszyny Wirtualnej systemu Windows w zestawie dostępności</span><span class="sxs-lookup"><span data-stu-id="4e1cf-115">Resize a Windows VM in an availability set</span></span>
<span data-ttu-id="4e1cf-116">Jeśli hello nowy rozmiar maszyny Wirtualnej w zestawie dostępności nie jest dostępne w klastrze sprzętu hello aktualnie obsługujący hello maszyny Wirtualnej, a następnie wszystkich maszyn wirtualnych w zestawie dostępności hello należy toobe alokację hello tooresize maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4e1cf-116">If hello new size for a VM in an availability set is not available on hello hardware cluster currently hosting hello VM, then all VMs in hello availability set will need toobe deallocated tooresize hello VM.</span></span> <span data-ttu-id="4e1cf-117">Należy również tooupdate hello rozmiar innych maszyn wirtualnych w dostępności powitania po jednej maszyny Wirtualnej został zmieniony.</span><span class="sxs-lookup"><span data-stu-id="4e1cf-117">You also might need tooupdate hello size of other VMs in hello availability set after one VM has been resized.</span></span> <span data-ttu-id="4e1cf-118">tooresize maszyny Wirtualnej w zestawie dostępności, wykonaj hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="4e1cf-118">tooresize a VM in an availability set, perform hello following steps.</span></span>

1. <span data-ttu-id="4e1cf-119">Wyświetl listę hello rozmiarów maszyn wirtualnych, które są dostępne na powitania sprzętu klastra, gdzie jest hostowana hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4e1cf-119">List hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span>
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. <span data-ttu-id="4e1cf-120">W razie potrzeby hello znajduje się rozmiar Uruchom hello następujące polecenia tooresize hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4e1cf-120">If hello desired size is listed, run hello following commands tooresize hello VM.</span></span> <span data-ttu-id="4e1cf-121">Jeśli nie ma na liście, przejdź toostep 3.</span><span class="sxs-lookup"><span data-stu-id="4e1cf-121">If it is not listed, go toostep 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="4e1cf-122">W razie potrzeby hello się, że nie ma rozmiar kontynuować hello następujące kroki toodeallocate wszystkich maszyn wirtualnych w zestawie dostępności hello, Zmień rozmiar maszyn wirtualnych i uruchomić je ponownie.</span><span class="sxs-lookup"><span data-stu-id="4e1cf-122">If hello desired size is not listed, continue with hello following steps toodeallocate all VMs in hello availability set, resize VMs, and restart them.</span></span>
4. <span data-ttu-id="4e1cf-123">Zatrzymanie wszystkich maszyn wirtualnych w zestawie dostępności hello.</span><span class="sxs-lookup"><span data-stu-id="4e1cf-123">Stop all VMs in hello availability set.</span></span>
   
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
5. <span data-ttu-id="4e1cf-124">Zmień rozmiar i ponownie uruchom hello maszyn wirtualnych w zestawie dostępności hello.</span><span class="sxs-lookup"><span data-stu-id="4e1cf-124">Resize and restart hello VMs in hello availability set.</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="4e1cf-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4e1cf-125">Next steps</span></span>
* <span data-ttu-id="4e1cf-126">Dodatkowe możliwości skalowania uruchamianie wielu wystąpień maszyny Wirtualnej i skalowanie w poziomie. Aby uzyskać więcej informacji, zobacz [automatycznie skalować w zestawie skalowania maszyn wirtualnych systemu Windows maszyny](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="4e1cf-126">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Windows machines in a Virtual Machine Scale Set](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span></span>

