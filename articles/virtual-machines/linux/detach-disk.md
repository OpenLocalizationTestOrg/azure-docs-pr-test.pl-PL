---
title: aaaDetach dysku danych maszyny wirtualnej systemu Linux - Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się toodetach dysku danych od maszyny wirtualnej na platformie Azure przy użyciu interfejsu wiersza polecenia w wersji 2.0 lub hello portalu Azure."
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
ms.openlocfilehash: 1c6145fc97f13179457225e93e0fb7adc261a65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-linux-virtual-machine"></a><span data-ttu-id="998fa-103">Jak toodetach danych na dysku od maszyny wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="998fa-103">How toodetach a data disk from a Linux virtual machine</span></span>

<span data-ttu-id="998fa-104">Jeśli nie ma potrzeby dysku danych, który jest dołączony tooa maszyny wirtualnej, możesz ją łatwo odłączyć.</span><span class="sxs-lookup"><span data-stu-id="998fa-104">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="998fa-105">Usuwa dysk hello z hello maszyny wirtualnej, ale nie powoduje usunięcia go z magazynu.</span><span class="sxs-lookup"><span data-stu-id="998fa-105">This removes hello disk from hello virtual machine, but doesn't remove it from storage.</span></span> 

> [!WARNING]
> <span data-ttu-id="998fa-106">Jeśli możesz odłączyć dysk, który nie jest automatycznie usuwana.</span><span class="sxs-lookup"><span data-stu-id="998fa-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="998fa-107">Jeśli masz subskrypcję magazynu tooPremium, będzie nadal opłaty za magazyn tooincur hello dysku.</span><span class="sxs-lookup"><span data-stu-id="998fa-107">If you have subscribed tooPremium storage, you will continue tooincur storage charges for hello disk.</span></span> <span data-ttu-id="998fa-108">Aby uzyskać więcej informacji można znaleźć zbyt[cennik i rozliczenia w przypadku korzystania z magazyn w warstwie Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="998fa-108">For more information refer too[Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span> 
> 
> 

<span data-ttu-id="998fa-109">Jeśli chcesz ponownie toouse hello istniejące dane na dysku hello, użytkownik może dołączyć go toohello tej samej maszyny wirtualnej lub innej.</span><span class="sxs-lookup"><span data-stu-id="998fa-109">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>  

## <a name="detach-a-data-disk-using-cli-20"></a><span data-ttu-id="998fa-110">Odłączyć dysku danych przy użyciu interfejsu wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="998fa-110">Detach a data disk using CLI 2.0</span></span>

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

<span data-ttu-id="998fa-111">dysk Hello pozostaje w pamięci masowej, ale nie jest już dołączony tooa maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="998fa-111">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>


## <a name="detach-a-data-disk-using-hello-portal"></a><span data-ttu-id="998fa-112">Odłączyć dysku danych przy użyciu portalu hello</span><span class="sxs-lookup"><span data-stu-id="998fa-112">Detach a data disk using hello portal</span></span>
1. <span data-ttu-id="998fa-113">W portalu Centrum hello, wybierz **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="998fa-113">In hello portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="998fa-114">Wybierz maszynę wirtualną hello, która ma dysk danych hello toodetach i kliknij **zatrzymać** hello toodeallocate maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="998fa-114">Select hello virtual machine that has hello data disk you want toodetach and click **Stop** toodeallocate hello VM.</span></span>
3. <span data-ttu-id="998fa-115">W bloku maszyny wirtualnej hello, wybierz **dysków**.</span><span class="sxs-lookup"><span data-stu-id="998fa-115">In hello virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="998fa-116">U góry hello hello **dysków** bloku, wybierz opcję **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="998fa-116">At hello top of hello **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="998fa-117">W hello **dysków** bloku toohello prawej krawędzi hello dysku danych chcesz toodetach, kliknij przycisk hello ![obraz przycisku Detach](./media/detach-disk/detach.png) odłączyć przycisku.</span><span class="sxs-lookup"><span data-stu-id="998fa-117">In hello **Disks** blade, toohello far right of hello data disk that you would like toodetach, click hello ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="998fa-118">Po usunięciu hello dysku, kliknij przycisk Zapisz u góry hello hello bloku.</span><span class="sxs-lookup"><span data-stu-id="998fa-118">After hello disk has been removed, click Save on hello top of hello blade.</span></span>
6. <span data-ttu-id="998fa-119">W bloku maszyny wirtualnej powitania kliknij **omówienie** , a następnie kliknij przycisk hello **Start** u góry hello hello bloku toorestart hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="998fa-119">In hello virtual machine blade, click **Overview** and then click hello **Start** button at hello top of hello blade toorestart hello VM.</span></span>

<span data-ttu-id="998fa-120">dysk Hello pozostaje w pamięci masowej, ale nie jest już dołączony tooa maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="998fa-120">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>








## <a name="next-steps"></a><span data-ttu-id="998fa-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="998fa-121">Next steps</span></span>
<span data-ttu-id="998fa-122">Jeśli chcesz dysku danych hello tooreuse został właśnie [dołączenie go tooanother wirtualna](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="998fa-122">If you want tooreuse hello data disk, you can just [attach it tooanother VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

