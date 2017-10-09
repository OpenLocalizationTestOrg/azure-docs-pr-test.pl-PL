---
title: aaaDetach dysku danych maszyny wirtualnej systemu Windows - Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się toodetach dysku danych od maszyny wirtualnej na platformie Azure przy użyciu modelu wdrażania usługi Resource Manager hello."
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
ms.openlocfilehash: f3f581d3f33329db2ecb7d25a68bc59af7361aad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-windows-virtual-machine"></a><span data-ttu-id="6a96a-103">Jak toodetach danych na dysku z maszyny wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="6a96a-103">How toodetach a data disk from a Windows virtual machine</span></span>
<span data-ttu-id="6a96a-104">Jeśli nie ma potrzeby dysku danych, który jest dołączony tooa maszyny wirtualnej, możesz ją łatwo odłączyć.</span><span class="sxs-lookup"><span data-stu-id="6a96a-104">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="6a96a-105">Usuwa dysk hello z hello maszyny wirtualnej, ale nie powoduje usunięcia go z magazynu.</span><span class="sxs-lookup"><span data-stu-id="6a96a-105">This removes hello disk from hello virtual machine, but doesn't remove it from storage.</span></span>

> [!WARNING]
> <span data-ttu-id="6a96a-106">Jeśli możesz odłączyć dysk, który nie jest automatycznie usuwana.</span><span class="sxs-lookup"><span data-stu-id="6a96a-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="6a96a-107">Jeśli masz subskrypcję magazynu tooPremium, będzie nadal opłaty za magazyn tooincur hello dysku.</span><span class="sxs-lookup"><span data-stu-id="6a96a-107">If you have subscribed tooPremium storage, you will continue tooincur storage charges for hello disk.</span></span> <span data-ttu-id="6a96a-108">Aby uzyskać więcej informacji można znaleźć zbyt[cennik i rozliczenia w przypadku korzystania z magazyn w warstwie Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="6a96a-108">For more information refer too[Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span>
>
>

<span data-ttu-id="6a96a-109">Jeśli chcesz ponownie toouse hello istniejące dane na dysku hello, użytkownik może dołączyć go toohello tej samej maszyny wirtualnej lub innej.</span><span class="sxs-lookup"><span data-stu-id="6a96a-109">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>

## <a name="detach-a-data-disk-using-hello-portal"></a><span data-ttu-id="6a96a-110">Odłączyć dysku danych przy użyciu portalu hello</span><span class="sxs-lookup"><span data-stu-id="6a96a-110">Detach a data disk using hello portal</span></span>
1. <span data-ttu-id="6a96a-111">W portalu Centrum hello, wybierz **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="6a96a-111">In hello portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="6a96a-112">Wybierz maszynę wirtualną hello, która ma dysk danych hello toodetach i kliknij **zatrzymać** hello toodeallocate maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6a96a-112">Select hello virtual machine that has hello data disk you want toodetach and click **Stop** toodeallocate hello VM.</span></span>
3. <span data-ttu-id="6a96a-113">W bloku maszyny wirtualnej hello, wybierz **dysków**.</span><span class="sxs-lookup"><span data-stu-id="6a96a-113">In hello virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="6a96a-114">U góry hello hello **dysków** bloku, wybierz opcję **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="6a96a-114">At hello top of hello **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="6a96a-115">W hello **dysków** bloku toohello prawej krawędzi hello dysku danych chcesz toodetach, kliknij przycisk hello ![obraz przycisku Detach](./media/detach-disk/detach.png) odłączyć przycisku.</span><span class="sxs-lookup"><span data-stu-id="6a96a-115">In hello **Disks** blade, toohello far right of hello data disk that you would like toodetach, click hello ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="6a96a-116">Po usunięciu hello dysku, kliknij przycisk Zapisz u góry hello hello bloku.</span><span class="sxs-lookup"><span data-stu-id="6a96a-116">After hello disk has been removed, click Save on hello top of hello blade.</span></span>
6. <span data-ttu-id="6a96a-117">W bloku maszyny wirtualnej powitania kliknij **omówienie** , a następnie kliknij przycisk hello **Start** u góry hello hello bloku toorestart hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6a96a-117">In hello virtual machine blade, click **Overview** and then click hello **Start** button at hello top of hello blade toorestart hello VM.</span></span>



<span data-ttu-id="6a96a-118">dysk Hello pozostaje w pamięci masowej, ale nie jest już dołączony tooa maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6a96a-118">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>

## <a name="detach-a-data-disk-using-powershell"></a><span data-ttu-id="6a96a-119">Odłączyć dysku danych przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="6a96a-119">Detach a data disk using PowerShell</span></span>
<span data-ttu-id="6a96a-120">W tym przykładzie hello pierwsze polecenie pobiera hello maszyny wirtualnej o nazwie **MyVM07** w hello **RG11** za pomocą polecenia cmdlet Get-AzureRmVM hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="6a96a-120">In this example, hello first command gets hello virtual machine named **MyVM07** in hello **RG11** resource group using hello Get-AzureRmVM cmdlet.</span></span> <span data-ttu-id="6a96a-121">Witaj polecenie sklepach hello maszyny wirtualnej w hello **$VirtualMachine** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="6a96a-121">hello command stores hello virtual machine in hello **$VirtualMachine** variable.</span></span>

<span data-ttu-id="6a96a-122">drugie polecenie Hello usuwa hello dysku danych o nazwie DataDisk3 z hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6a96a-122">hello second command removes hello data disk named DataDisk3 from hello virtual machine.</span></span>

<span data-ttu-id="6a96a-123">polecenie końcowego Hello aktualizuje stan hello hello maszyny wirtualnej toocomplete hello proces usuwania dysku z danymi hello.</span><span class="sxs-lookup"><span data-stu-id="6a96a-123">hello final command updates hello state of hello virtual machine toocomplete hello process of removing hello data disk.</span></span>

```powershell
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07"
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "DataDisk3"
Update-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" -VM $VirtualMachine
```

<span data-ttu-id="6a96a-124">Aby uzyskać więcej informacji, zobacz [AzureRmVMDataDisk Usuń](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span><span class="sxs-lookup"><span data-stu-id="6a96a-124">For more information, see [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a96a-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6a96a-125">Next steps</span></span>
<span data-ttu-id="6a96a-126">Jeśli chcesz dysku danych hello tooreuse został właśnie [dołączenie go tooanother maszyny Wirtualnej](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="6a96a-126">If you want tooreuse hello data disk, you can just [attach it tooanother VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

