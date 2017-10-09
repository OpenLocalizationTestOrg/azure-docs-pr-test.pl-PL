---
title: aaaAttach tooa dysku danych maszyny Wirtualnej systemu Linux | Dokumentacja firmy Microsoft
description: "Jak tooattach danych nowego lub istniejącego dysku tooa maszyny Wirtualnej systemu Linux w hello przy użyciu portalu Azure hello modelu wdrażania usługi Resource Manager."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5e1c6212-976c-4962-a297-177942f90907
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: cynthn
ms.openlocfilehash: 069c3c6f5e71a8c495342e6d0c6f3d92c4ed5053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-vm-in-hello-azure-portal"></a><span data-ttu-id="1f353-103">Jak tooattach danych na dysku tooa maszyny Wirtualnej systemu Linux w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="1f353-103">How tooattach a data disk tooa Linux VM in hello Azure portal</span></span>
<span data-ttu-id="1f353-104">W tym artykule opisano, jak tooattach istniejących i nowych dysków maszyny wirtualnej systemu Linux tooa za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1f353-104">This article shows you how tooattach both new and existing disks tooa Linux virtual machine through hello Azure portal.</span></span> <span data-ttu-id="1f353-105">Możesz również [dołączyć tooa dysku danych maszyny Wirtualnej systemu Windows w portalu Azure hello](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1f353-105">You can also [attach a data disk tooa Windows VM in hello Azure portal](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="1f353-106">Możesz wybrać toouse albo Azure dysków zarządzanych lub niezarządzanych dysków.</span><span class="sxs-lookup"><span data-stu-id="1f353-106">You can choose toouse either Azure Managed Disks or unmanaged disks.</span></span> <span data-ttu-id="1f353-107">Zarządzane dyski są obsługiwane przez hello platformy Azure i nie wymagają żadnych toostore przygotowania lub lokalizacji je.</span><span class="sxs-lookup"><span data-stu-id="1f353-107">Managed disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="1f353-108">Niezarządzane dyski wymagają konta magazynu i mają pewne [przydziały i ograniczenia, które są stosowane](../../azure-subscription-service-limits.md#storage-limits).</span><span class="sxs-lookup"><span data-stu-id="1f353-108">Unmanaged disks require a storage account and have some [quotas and limits that apply](../../azure-subscription-service-limits.md#storage-limits).</span></span> <span data-ttu-id="1f353-109">Aby uzyskać więcej informacji o dyskach Azure Managed Disks, zobacz [Omówienie usługi Azure Managed Disks](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1f353-109">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="1f353-110">Przed dołączeniem tooyour dysków maszyny Wirtualnej, przejrzyj te wskazówki:</span><span class="sxs-lookup"><span data-stu-id="1f353-110">Before you attach disks tooyour VM, review these tips:</span></span>

* <span data-ttu-id="1f353-111">Hello rozmiar maszyny wirtualnej hello Określa, ile można dołączać dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="1f353-111">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="1f353-112">Aby uzyskać więcej informacji, zobacz [rozmiary maszyn wirtualnych](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1f353-112">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="1f353-113">Magazyn w warstwie Premium toouse, należy serii DS lub GS-series maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1f353-113">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="1f353-114">Można użyć zarówno Premium i standardowa dysków z tych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="1f353-114">You can use both Premium and Standard disks with these virtual machines.</span></span> <span data-ttu-id="1f353-115">Magazyn w warstwie Premium jest dostępna w pewnych regionach.</span><span class="sxs-lookup"><span data-stu-id="1f353-115">Premium storage is available in certain regions.</span></span> <span data-ttu-id="1f353-116">Aby uzyskać więcej informacji, zobacz [magazyn w warstwie Premium: magazyn o wysokiej wydajności dla obciążeń maszyny wirtualnej Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1f353-116">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="1f353-117">Maszyny toovirtual dołączone dyski są faktycznie pliki VHD przechowywane na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="1f353-117">Disks attached toovirtual machines are actually .vhd files stored in Azure.</span></span> <span data-ttu-id="1f353-118">Aby uzyskać więcej informacji, zobacz [o dyskach i wirtualne dyski twarde dla maszyn wirtualnych](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1f353-118">For details, see [About disks and VHDs for virtual machines](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="find-hello-virtual-machine"></a><span data-ttu-id="1f353-119">Znajdź hello maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1f353-119">Find hello virtual machine</span></span>
1. <span data-ttu-id="1f353-120">Zaloguj się toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1f353-120">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1f353-121">W menu Centrum powitania kliknij **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="1f353-121">On hello Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="1f353-122">Wybierz maszynę wirtualną hello z listy hello.</span><span class="sxs-lookup"><span data-stu-id="1f353-122">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="1f353-123">toohello wirtualnej maszyny bloku, w **Essentials**, kliknij przycisk **dysków**.</span><span class="sxs-lookup"><span data-stu-id="1f353-123">toohello Virtual machines blade, in **Essentials**, click **Disks**.</span></span>
   
    ![Otwórz ustawienia dysku](./media/attach-disk-portal/find-disk-settings.png)

<span data-ttu-id="1f353-125">Kontynuuj przez następujące instrukcje dotyczące dołączania albo [dysków zarządzanych w](#use-azure-managed-disks) lub [niezarządzane dysku](#use-unmanaged-disks).</span><span class="sxs-lookup"><span data-stu-id="1f353-125">Continue by following instructions for attaching either a [managed disk](#use-azure-managed-disks) or [unmanaged disk](#use-unmanaged-disks).</span></span>

## <a name="use-azure-managed-disks"></a><span data-ttu-id="1f353-126">Użyj zarządzanego dysku systemu Azure</span><span class="sxs-lookup"><span data-stu-id="1f353-126">Use Azure Managed Disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="1f353-127">Dołączanie nowego dysku</span><span class="sxs-lookup"><span data-stu-id="1f353-127">Attach a new disk</span></span>

1. <span data-ttu-id="1f353-128">Na powitania **dysków** bloku, kliknij przycisk **+ Dodaj dysk danych**.</span><span class="sxs-lookup"><span data-stu-id="1f353-128">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="1f353-129">Kliknij menu rozwijanego hello **nazwa** i wybierz **Tworzenie dysku**:</span><span class="sxs-lookup"><span data-stu-id="1f353-129">Click hello drop-down menu for **Name** and select **Create disk**:</span></span>

    ![Utwórz Azure dysków zarządzanych](./media/attach-disk-portal/create-new-md.png)

3. <span data-ttu-id="1f353-131">Wprowadź nazwę dysku zarządzanego.</span><span class="sxs-lookup"><span data-stu-id="1f353-131">Enter a name for your managed disk.</span></span> <span data-ttu-id="1f353-132">Przejrzyj ustawienia domyślne hello, zaktualizuj odpowiednio do potrzeb, a następnie kliknij **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1f353-132">Review hello default settings, update as necessary, and then click **Create**.</span></span>
   
   ![Przejrzyj ustawienia dysku](./media/attach-disk-portal/create-new-md-settings.png)

4. <span data-ttu-id="1f353-134">Kliknij przycisk **zapisać** toocreate hello zarządzane dysku i aktualizacji konfiguracji maszyny Wirtualnej hello:</span><span class="sxs-lookup"><span data-stu-id="1f353-134">Click **Save** toocreate hello managed disk and update hello VM configuration:</span></span>

   ![Zapisz nowy dysk zarządzane Azure](./media/attach-disk-portal/confirm-create-new-md.png)

5. <span data-ttu-id="1f353-136">Po Azure tworzy dysk hello i dołącza go toohello maszyny wirtualnej, hello nowego dysku jest wymieniony w ustawienia dysku maszyny wirtualnej hello w obszarze **dysków z danymi**.</span><span class="sxs-lookup"><span data-stu-id="1f353-136">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span> <span data-ttu-id="1f353-137">Dyski zarządzane są zasobem najwyższego poziomu, hello dysk zostanie wyświetlony w głównym hello hello grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="1f353-137">As managed disks are a top-level resource, hello disk appears at hello root of hello resource group:</span></span>

   ![Dysku platformy Azure zarządzanych w grupie zasobów](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a><span data-ttu-id="1f353-139">Dołączanie istniejącego dysku</span><span class="sxs-lookup"><span data-stu-id="1f353-139">Attach an existing disk</span></span>
1. <span data-ttu-id="1f353-140">Na powitania **dysków** bloku, kliknij przycisk **+ Dodaj dysk danych**.</span><span class="sxs-lookup"><span data-stu-id="1f353-140">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="1f353-141">Kliknij menu rozwijanego hello **nazwa** tooview listę istniejących zarządzane tooyour dostępne dyski subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1f353-141">Click hello drop-down menu for **Name** tooview a list of existing managed disks accessible tooyour Azure subscription.</span></span> <span data-ttu-id="1f353-142">Wybierz hello zarządzane tooattach dysku:</span><span class="sxs-lookup"><span data-stu-id="1f353-142">Select hello managed disk tooattach:</span></span>

   ![Dołączanie istniejącego dysku zarządzanego Azure](./media/attach-disk-portal/select-existing-md.png)

3. <span data-ttu-id="1f353-144">Kliknij przycisk **zapisać** istniejących hello tooattach zarządzane dysku i aktualizacji konfiguracji maszyny Wirtualnej hello:</span><span class="sxs-lookup"><span data-stu-id="1f353-144">Click **Save** tooattach hello existing managed disk and update hello VM configuration:</span></span>
   
   ![Zapisanie aktualizacji dysku zarządzanego Azure](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. <span data-ttu-id="1f353-146">Po Azure dołącza hello maszyny wirtualnej toohello dysku, znajduje się w ustawieniach dysku maszyny wirtualnej hello w obszarze **dysków z danymi**.</span><span class="sxs-lookup"><span data-stu-id="1f353-146">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-unmanaged-disks"></a><span data-ttu-id="1f353-147">Niezarządzane dysków</span><span class="sxs-lookup"><span data-stu-id="1f353-147">Use unmanaged disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="1f353-148">Dołączanie nowego dysku</span><span class="sxs-lookup"><span data-stu-id="1f353-148">Attach a new disk</span></span>

1. <span data-ttu-id="1f353-149">Na powitania **dysków** bloku, kliknij przycisk **+ Dodaj dysk danych**.</span><span class="sxs-lookup"><span data-stu-id="1f353-149">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="1f353-150">Przejrzyj ustawienia domyślne hello, zaktualizuj odpowiednio do potrzeb, a następnie kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="1f353-150">Review hello default settings, update as necessary, and then click **OK**.</span></span>
   
   ![Przejrzyj ustawienia dysku](./media/attach-disk-portal/attach-new.png)
3. <span data-ttu-id="1f353-152">Po Azure tworzy dysk hello i dołącza go toohello maszyny wirtualnej, hello nowego dysku jest wymieniony w ustawienia dysku maszyny wirtualnej hello w obszarze **dysków z danymi**.</span><span class="sxs-lookup"><span data-stu-id="1f353-152">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="attach-an-existing-disk"></a><span data-ttu-id="1f353-153">Dołączanie istniejącego dysku</span><span class="sxs-lookup"><span data-stu-id="1f353-153">Attach an existing disk</span></span>
1. <span data-ttu-id="1f353-154">Na powitania **dysków** bloku, kliknij przycisk **+ Dodaj dysk danych**.</span><span class="sxs-lookup"><span data-stu-id="1f353-154">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="1f353-155">W obszarze **dołączyć istniejącego dysku**, kliknij przycisk **pliku VHD**.</span><span class="sxs-lookup"><span data-stu-id="1f353-155">Under **Attach existing disk**, click **VHD File**.</span></span>
   
   ![Dołączanie istniejącego dysku](./media/attach-disk-portal/attach-existing.png)
3. <span data-ttu-id="1f353-157">W obszarze **kont magazynu**, wybierz konto hello i kontener, który zawiera plik VHD hello.</span><span class="sxs-lookup"><span data-stu-id="1f353-157">Under **Storage accounts**, select hello account and container that holds hello .vhd file.</span></span>
   
   ![Znajdź lokalizację wirtualnego dysku twardego](./media/attach-disk-portal/find-storage-container.png)
4. <span data-ttu-id="1f353-159">Wybierz plik VHD hello.</span><span class="sxs-lookup"><span data-stu-id="1f353-159">Select hello .vhd file.</span></span>
5. <span data-ttu-id="1f353-160">W obszarze **dołączyć istniejącego dysku**, po prostu wybrany plik hello jest wyświetlana w obszarze **pliku VHD**.</span><span class="sxs-lookup"><span data-stu-id="1f353-160">Under **Attach existing disk**, hello file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="1f353-161">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1f353-161">Click **OK**.</span></span>
6. <span data-ttu-id="1f353-162">Po Azure dołącza hello maszyny wirtualnej toohello dysku, znajduje się w ustawieniach dysku maszyny wirtualnej hello w obszarze **dysków z danymi**.</span><span class="sxs-lookup"><span data-stu-id="1f353-162">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1f353-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1f353-163">Next steps</span></span>
<span data-ttu-id="1f353-164">Po dodaniu dysku hello należy tooprepare go do użycia.</span><span class="sxs-lookup"><span data-stu-id="1f353-164">After hello disk is added, you need tooprepare it for use.</span></span> <span data-ttu-id="1f353-165">Aby uzyskać więcej informacji, zobacz [porady: inicjowanie nowy dysk danych w systemie Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="1f353-165">For more information, see [How to: Initialize a new data disk in Linux](add-disk.md).</span></span>
