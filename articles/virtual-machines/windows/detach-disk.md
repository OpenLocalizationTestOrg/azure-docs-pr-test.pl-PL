---
title: "Odłączyć dysku danych maszyny wirtualnej systemu Windows - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się odłączyć dysku danych z maszyny wirtualnej na platformie Azure przy użyciu modelu wdrażania Menedżera zasobów."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 13180343-ac49-4a3a-85d8-0ead95e2028c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 97aa69745d200ee76f9f859eb3a8b0ad2f202bad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-detach-a-data-disk-from-a-windows-virtual-machine"></a><span data-ttu-id="cc9f2-103">Jak można odłączyć dysku danych od maszyny wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="cc9f2-103">How to detach a data disk from a Windows virtual machine</span></span>
<span data-ttu-id="cc9f2-104">Gdy już nie potrzebujesz dysku danych dołączonego do maszyny wirtualnej, możesz go łatwo odłączyć.</span><span class="sxs-lookup"><span data-stu-id="cc9f2-104">When you no longer need a data disk that's attached to a virtual machine, you can easily detach it.</span></span> <span data-ttu-id="cc9f2-105">Usuwa dysk od maszyny wirtualnej, ale nie powoduje usunięcia go z magazynu.</span><span class="sxs-lookup"><span data-stu-id="cc9f2-105">This removes the disk from the virtual machine, but doesn't remove it from storage.</span></span>

> [!WARNING]
> <span data-ttu-id="cc9f2-106">Jeśli możesz odłączyć dysk, który nie jest automatycznie usuwana.</span><span class="sxs-lookup"><span data-stu-id="cc9f2-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="cc9f2-107">Jeśli masz subskrypcję do magazyn w warstwie Premium, będą nadal naliczane opłaty za magazyn dla dysku.</span><span class="sxs-lookup"><span data-stu-id="cc9f2-107">If you have subscribed to Premium storage, you will continue to incur storage charges for the disk.</span></span> <span data-ttu-id="cc9f2-108">Więcej informacji można znaleźć w [cennik i rozliczenia w przypadku korzystania z magazyn w warstwie Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="cc9f2-108">For more information refer to [Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span>
>
>

<span data-ttu-id="cc9f2-109">Jeśli chcesz użyć danych znajdujących się na tym dysku, możesz dołączyć go ponownie do tej samej lub innej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cc9f2-109">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.</span></span>

## <a name="detach-a-data-disk-using-the-portal"></a><span data-ttu-id="cc9f2-110">Odłączanie dysku danych przy użyciu portalu</span><span class="sxs-lookup"><span data-stu-id="cc9f2-110">Detach a data disk using the portal</span></span>
1. <span data-ttu-id="cc9f2-111">W Centrum w portalu, wybierz **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="cc9f2-111">In the portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="cc9f2-112">Wybierz maszynę wirtualną, która ma dysk danych, aby odłączyć, a następnie kliknij przycisk **zatrzymać** można cofnąć alokacji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cc9f2-112">Select the virtual machine that has the data disk you want to detach and click **Stop** to deallocate the VM.</span></span>
3. <span data-ttu-id="cc9f2-113">W bloku maszyny wirtualnej, wybierz **dysków**.</span><span class="sxs-lookup"><span data-stu-id="cc9f2-113">In the virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="cc9f2-114">W górnej części **dysków** bloku, wybierz opcję **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="cc9f2-114">At the top of the **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="cc9f2-115">W **dysków** bloku do prawej krawędzi dysk z danymi, które chcesz odłączyć, kliknij przycisk ![obraz przycisku Detach](./media/detach-disk/detach.png) odłączyć przycisku.</span><span class="sxs-lookup"><span data-stu-id="cc9f2-115">In the **Disks** blade, to the far right of the data disk that you would like to detach, click the ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="cc9f2-116">Po usunięciu dysk, kliknij przycisk Zapisz w górnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="cc9f2-116">After the disk has been removed, click Save on the top of the blade.</span></span>
6. <span data-ttu-id="cc9f2-117">W bloku maszyny wirtualnej, kliknij przycisk **omówienie** , a następnie kliknij przycisk **Start** na górze bloku, aby ponownie uruchomić maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cc9f2-117">In the virtual machine blade, click **Overview** and then click the **Start** button at the top of the blade to restart the VM.</span></span>



<span data-ttu-id="cc9f2-118">Odłączony dysk pozostaje w magazynie, lecz nie jest już dołączony do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cc9f2-118">The disk remains in storage but is no longer attached to a virtual machine.</span></span>

## <a name="detach-a-data-disk-using-powershell"></a><span data-ttu-id="cc9f2-119">Odłączyć dysku danych przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc9f2-119">Detach a data disk using PowerShell</span></span>
<span data-ttu-id="cc9f2-120">W tym przykładzie pierwsze polecenie pobiera maszyny wirtualnej o nazwie **MyVM07** w **RG11** za pomocą polecenia cmdlet Get-AzureRmVM grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="cc9f2-120">In this example, the first command gets the virtual machine named **MyVM07** in the **RG11** resource group using the Get-AzureRmVM cmdlet.</span></span> <span data-ttu-id="cc9f2-121">Polecenie przechowuje maszynę wirtualną w **$VirtualMachine** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="cc9f2-121">The command stores the virtual machine in the **$VirtualMachine** variable.</span></span>

<span data-ttu-id="cc9f2-122">Drugie polecenie usuwa dysku danych o nazwie DataDisk3 z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cc9f2-122">The second command removes the data disk named DataDisk3 from the virtual machine.</span></span>

<span data-ttu-id="cc9f2-123">Polecenia końcowego aktualizuje stan maszyny wirtualnej, aby ukończyć proces usuwania dysk z danymi.</span><span class="sxs-lookup"><span data-stu-id="cc9f2-123">The final command updates the state of the virtual machine to complete the process of removing the data disk.</span></span>

```powershell
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07"
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "DataDisk3"
Update-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" -VM $VirtualMachine
```

<span data-ttu-id="cc9f2-124">Aby uzyskać więcej informacji, zobacz [AzureRmVMDataDisk Usuń](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span><span class="sxs-lookup"><span data-stu-id="cc9f2-124">For more information, see [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc9f2-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cc9f2-125">Next steps</span></span>
<span data-ttu-id="cc9f2-126">Jeśli chcesz ponownie użyć dysku danych, możesz po prostu [dołączenie go do innej maszyny Wirtualnej](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="cc9f2-126">If you want to reuse the data disk, you can just [attach it to another VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

