---
title: "Odłączyć dysku danych maszyny wirtualnej systemu Linux - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się odłączyć dysku danych z maszyny wirtualnej na platformie Azure przy użyciu interfejsu wiersza polecenia w wersji 2.0 lub portalu Azure."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: azurecli
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 3f29547e1da6028b1e4b91d9e29fd3bcdfe08d50
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-detach-a-data-disk-from-a-linux-virtual-machine"></a><span data-ttu-id="e0c8f-103">Jak można odłączyć dysku danych od maszyny wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="e0c8f-103">How to detach a data disk from a Linux virtual machine</span></span>

<span data-ttu-id="e0c8f-104">Gdy już nie potrzebujesz dysku danych dołączonego do maszyny wirtualnej, możesz go łatwo odłączyć.</span><span class="sxs-lookup"><span data-stu-id="e0c8f-104">When you no longer need a data disk that's attached to a virtual machine, you can easily detach it.</span></span> <span data-ttu-id="e0c8f-105">Usuwa dysk od maszyny wirtualnej, ale nie powoduje usunięcia go z magazynu.</span><span class="sxs-lookup"><span data-stu-id="e0c8f-105">This removes the disk from the virtual machine, but doesn't remove it from storage.</span></span> 

> [!WARNING]
> <span data-ttu-id="e0c8f-106">Jeśli możesz odłączyć dysk, który nie jest automatycznie usuwana.</span><span class="sxs-lookup"><span data-stu-id="e0c8f-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="e0c8f-107">Jeśli masz subskrypcję do magazyn w warstwie Premium, będą nadal naliczane opłaty za magazyn dla dysku.</span><span class="sxs-lookup"><span data-stu-id="e0c8f-107">If you have subscribed to Premium storage, you will continue to incur storage charges for the disk.</span></span> <span data-ttu-id="e0c8f-108">Więcej informacji można znaleźć w [cennik i rozliczenia w przypadku korzystania z magazyn w warstwie Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="e0c8f-108">For more information refer to [Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span> 
> 
> 

<span data-ttu-id="e0c8f-109">Jeśli chcesz użyć danych znajdujących się na tym dysku, możesz dołączyć go ponownie do tej samej lub innej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e0c8f-109">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.</span></span>  

## <a name="detach-a-data-disk-using-cli-20"></a><span data-ttu-id="e0c8f-110">Odłączyć dysku danych przy użyciu interfejsu wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="e0c8f-110">Detach a data disk using CLI 2.0</span></span>

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

<span data-ttu-id="e0c8f-111">Odłączony dysk pozostaje w magazynie, lecz nie jest już dołączony do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e0c8f-111">The disk remains in storage but is no longer attached to a virtual machine.</span></span>


## <a name="detach-a-data-disk-using-the-portal"></a><span data-ttu-id="e0c8f-112">Odłączanie dysku danych przy użyciu portalu</span><span class="sxs-lookup"><span data-stu-id="e0c8f-112">Detach a data disk using the portal</span></span>
1. <span data-ttu-id="e0c8f-113">W Centrum w portalu, wybierz **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="e0c8f-113">In the portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="e0c8f-114">Wybierz maszynę wirtualną, która ma dysk danych, aby odłączyć, a następnie kliknij przycisk **zatrzymać** można cofnąć alokacji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e0c8f-114">Select the virtual machine that has the data disk you want to detach and click **Stop** to deallocate the VM.</span></span>
3. <span data-ttu-id="e0c8f-115">W bloku maszyny wirtualnej, wybierz **dysków**.</span><span class="sxs-lookup"><span data-stu-id="e0c8f-115">In the virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="e0c8f-116">W górnej części **dysków** bloku, wybierz opcję **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="e0c8f-116">At the top of the **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="e0c8f-117">W **dysków** bloku do prawej krawędzi dysk z danymi, które chcesz odłączyć, kliknij przycisk ![obraz przycisku Detach](./media/detach-disk/detach.png) odłączyć przycisku.</span><span class="sxs-lookup"><span data-stu-id="e0c8f-117">In the **Disks** blade, to the far right of the data disk that you would like to detach, click the ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="e0c8f-118">Po usunięciu dysk, kliknij przycisk Zapisz w górnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="e0c8f-118">After the disk has been removed, click Save on the top of the blade.</span></span>
6. <span data-ttu-id="e0c8f-119">W bloku maszyny wirtualnej, kliknij przycisk **omówienie** , a następnie kliknij przycisk **Start** na górze bloku, aby ponownie uruchomić maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e0c8f-119">In the virtual machine blade, click **Overview** and then click the **Start** button at the top of the blade to restart the VM.</span></span>

<span data-ttu-id="e0c8f-120">Odłączony dysk pozostaje w magazynie, lecz nie jest już dołączony do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e0c8f-120">The disk remains in storage but is no longer attached to a virtual machine.</span></span>








## <a name="next-steps"></a><span data-ttu-id="e0c8f-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e0c8f-121">Next steps</span></span>
<span data-ttu-id="e0c8f-122">Jeśli chcesz ponownie użyć dysku danych, możesz po prostu [dołączenie go do innej maszyny Wirtualnej](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e0c8f-122">If you want to reuse the data disk, you can just [attach it to another VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

