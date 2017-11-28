---
title: "Dołączenie dysku danych do maszyny Wirtualnej systemu Linux | Dokumentacja firmy Microsoft"
description: "Jak można dołączyć danych do nowego lub istniejącego dysku do maszyny Wirtualnej systemu Linux, w portalu Azure przy użyciu modelu wdrażania Menedżera zasobów."
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
ms.openlocfilehash: 1599ee241c3d9fb3623ebd89ae30f2795cae1930
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-attach-a-data-disk-to-a-linux-vm-in-the-azure-portal"></a><span data-ttu-id="d795c-103">Jak można dołączyć dysku danych do maszyny Wirtualnej systemu Linux, w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d795c-103">How to attach a data disk to a Linux VM in the Azure portal</span></span>
<span data-ttu-id="d795c-104">W tym artykule przedstawiono sposób dołączyć istniejących i nowych dysków do maszyny wirtualnej systemu Linux za pośrednictwem portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d795c-104">This article shows you how to attach both new and existing disks to a Linux virtual machine through the Azure portal.</span></span> <span data-ttu-id="d795c-105">Możesz również [dołączenie dysku danych do maszyny Wirtualnej systemu Windows w portalu Azure](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d795c-105">You can also [attach a data disk to a Windows VM in the Azure portal](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="d795c-106">Można użyć Azure dysków zarządzane lub niezarządzane dysków.</span><span class="sxs-lookup"><span data-stu-id="d795c-106">You can choose to use either Azure Managed Disks or unmanaged disks.</span></span> <span data-ttu-id="d795c-107">Dyski zarządzane są obsługiwane przez platformę Azure i nie wymagają wszystkie lub lokalizację do przechowywania ich.</span><span class="sxs-lookup"><span data-stu-id="d795c-107">Managed disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="d795c-108">Niezarządzane dyski wymagają konta magazynu i mają pewne [przydziały i ograniczenia, które są stosowane](../../azure-subscription-service-limits.md#storage-limits).</span><span class="sxs-lookup"><span data-stu-id="d795c-108">Unmanaged disks require a storage account and have some [quotas and limits that apply](../../azure-subscription-service-limits.md#storage-limits).</span></span> <span data-ttu-id="d795c-109">Aby uzyskać więcej informacji o dyskach Azure Managed Disks, zobacz [Omówienie usługi Azure Managed Disks](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d795c-109">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="d795c-110">Przed dołączeniem dysków do maszyny Wirtualnej, przejrzyj następujące wskazówki:</span><span class="sxs-lookup"><span data-stu-id="d795c-110">Before you attach disks to your VM, review these tips:</span></span>

* <span data-ttu-id="d795c-111">Rozmiar maszyny wirtualnej Określa, ile można dołączać dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="d795c-111">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="d795c-112">Aby uzyskać więcej informacji, zobacz [rozmiary maszyn wirtualnych](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d795c-112">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="d795c-113">Aby użyć magazyn w warstwie Premium, należy serii DS lub GS-series maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d795c-113">To use Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="d795c-114">Można użyć zarówno Premium i standardowa dysków z tych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="d795c-114">You can use both Premium and Standard disks with these virtual machines.</span></span> <span data-ttu-id="d795c-115">Magazyn w warstwie Premium jest dostępna w pewnych regionach.</span><span class="sxs-lookup"><span data-stu-id="d795c-115">Premium storage is available in certain regions.</span></span> <span data-ttu-id="d795c-116">Aby uzyskać więcej informacji, zobacz [magazyn w warstwie Premium: magazyn o wysokiej wydajności dla obciążeń maszyny wirtualnej Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d795c-116">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="d795c-117">Dysków dołączonych do maszyn wirtualnych są faktycznie pliki VHD przechowywane na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d795c-117">Disks attached to virtual machines are actually .vhd files stored in Azure.</span></span> <span data-ttu-id="d795c-118">Aby uzyskać więcej informacji, zobacz [o dyskach i wirtualne dyski twarde dla maszyn wirtualnych](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d795c-118">For details, see [About disks and VHDs for virtual machines](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="find-the-virtual-machine"></a><span data-ttu-id="d795c-119">Znaleźć maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d795c-119">Find the virtual machine</span></span>
1. <span data-ttu-id="d795c-120">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d795c-120">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d795c-121">W menu Centrum kliknij pozycję **Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="d795c-121">On the Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="d795c-122">Wybierz maszynę wirtualną z listy.</span><span class="sxs-lookup"><span data-stu-id="d795c-122">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="d795c-123">Do wirtualnej maszyny bloku, w **Essentials**, kliknij przycisk **dysków**.</span><span class="sxs-lookup"><span data-stu-id="d795c-123">To the Virtual machines blade, in **Essentials**, click **Disks**.</span></span>
   
    ![Otwórz ustawienia dysku](./media/attach-disk-portal/find-disk-settings.png)

<span data-ttu-id="d795c-125">Kontynuuj przez następujące instrukcje dotyczące dołączania albo [dysków zarządzanych w](#use-azure-managed-disks) lub [niezarządzane dysku](#use-unmanaged-disks).</span><span class="sxs-lookup"><span data-stu-id="d795c-125">Continue by following instructions for attaching either a [managed disk](#use-azure-managed-disks) or [unmanaged disk](#use-unmanaged-disks).</span></span>

## <a name="use-azure-managed-disks"></a><span data-ttu-id="d795c-126">Użyj zarządzanego dysku systemu Azure</span><span class="sxs-lookup"><span data-stu-id="d795c-126">Use Azure Managed Disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="d795c-127">Dołączanie nowego dysku</span><span class="sxs-lookup"><span data-stu-id="d795c-127">Attach a new disk</span></span>

1. <span data-ttu-id="d795c-128">Na **dysków** bloku, kliknij przycisk **+ Dodaj dysk danych**.</span><span class="sxs-lookup"><span data-stu-id="d795c-128">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="d795c-129">Kliknij menu rozwijane dla **nazwa** i wybierz **Tworzenie dysku**:</span><span class="sxs-lookup"><span data-stu-id="d795c-129">Click the drop-down menu for **Name** and select **Create disk**:</span></span>

    ![Utwórz Azure dysków zarządzanych](./media/attach-disk-portal/create-new-md.png)

3. <span data-ttu-id="d795c-131">Wprowadź nazwę dysku zarządzanego.</span><span class="sxs-lookup"><span data-stu-id="d795c-131">Enter a name for your managed disk.</span></span> <span data-ttu-id="d795c-132">Przejrzyj ustawienia domyślne, należy zaktualizować odpowiednio do potrzeb, a następnie kliknij **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d795c-132">Review the default settings, update as necessary, and then click **Create**.</span></span>
   
   ![Przejrzyj ustawienia dysku](./media/attach-disk-portal/create-new-md-settings.png)

4. <span data-ttu-id="d795c-134">Kliknij przycisk **zapisać** do tworzenia dysków zarządzanych i aktualizowania konfiguracji maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="d795c-134">Click **Save** to create the managed disk and update the VM configuration:</span></span>

   ![Zapisz nowy dysk zarządzane Azure](./media/attach-disk-portal/confirm-create-new-md.png)

5. <span data-ttu-id="d795c-136">Po Azure utworzy dysk i dołącza go do maszyny wirtualnej, nowy dysk ma na liście ustawień dysku maszyny wirtualnej w obszarze **dysków z danymi**.</span><span class="sxs-lookup"><span data-stu-id="d795c-136">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span> <span data-ttu-id="d795c-137">Dyski zarządzane są zasobem najwyższego poziomu dysku pojawia się w katalogu głównym grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="d795c-137">As managed disks are a top-level resource, the disk appears at the root of the resource group:</span></span>

   ![Dysku platformy Azure zarządzanych w grupie zasobów](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a><span data-ttu-id="d795c-139">Dołączanie istniejącego dysku</span><span class="sxs-lookup"><span data-stu-id="d795c-139">Attach an existing disk</span></span>
1. <span data-ttu-id="d795c-140">Na **dysków** bloku, kliknij przycisk **+ Dodaj dysk danych**.</span><span class="sxs-lookup"><span data-stu-id="d795c-140">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="d795c-141">Kliknij menu rozwijane dla **nazwa** Aby wyświetlić listę istniejących dysków zarządzanych dostępny dla Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d795c-141">Click the drop-down menu for **Name** to view a list of existing managed disks accessible to your Azure subscription.</span></span> <span data-ttu-id="d795c-142">Wybierz zarządzane dysku, aby dołączyć:</span><span class="sxs-lookup"><span data-stu-id="d795c-142">Select the managed disk to attach:</span></span>

   ![Dołączanie istniejącego dysku zarządzanego Azure](./media/attach-disk-portal/select-existing-md.png)

3. <span data-ttu-id="d795c-144">Kliknij przycisk **zapisać** dołączyć istniejącego dysku zarządzanego i zaktualizować konfiguracji maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="d795c-144">Click **Save** to attach the existing managed disk and update the VM configuration:</span></span>
   
   ![Zapisanie aktualizacji dysku zarządzanego Azure](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. <span data-ttu-id="d795c-146">Po Azure dołącza dysk do maszyny wirtualnej, jest wymienione w ustawieniach dysku maszyny wirtualnej w obszarze **dysków z danymi**.</span><span class="sxs-lookup"><span data-stu-id="d795c-146">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-unmanaged-disks"></a><span data-ttu-id="d795c-147">Niezarządzane dysków</span><span class="sxs-lookup"><span data-stu-id="d795c-147">Use unmanaged disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="d795c-148">Dołączanie nowego dysku</span><span class="sxs-lookup"><span data-stu-id="d795c-148">Attach a new disk</span></span>

1. <span data-ttu-id="d795c-149">Na **dysków** bloku, kliknij przycisk **+ Dodaj dysk danych**.</span><span class="sxs-lookup"><span data-stu-id="d795c-149">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="d795c-150">Przejrzyj ustawienia domyślne, należy zaktualizować odpowiednio do potrzeb, a następnie kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="d795c-150">Review the default settings, update as necessary, and then click **OK**.</span></span>
   
   ![Przejrzyj ustawienia dysku](./media/attach-disk-portal/attach-new.png)
3. <span data-ttu-id="d795c-152">Po Azure utworzy dysk i dołącza go do maszyny wirtualnej, nowy dysk ma na liście ustawień dysku maszyny wirtualnej w obszarze **dysków z danymi**.</span><span class="sxs-lookup"><span data-stu-id="d795c-152">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="attach-an-existing-disk"></a><span data-ttu-id="d795c-153">Dołączanie istniejącego dysku</span><span class="sxs-lookup"><span data-stu-id="d795c-153">Attach an existing disk</span></span>
1. <span data-ttu-id="d795c-154">Na **dysków** bloku, kliknij przycisk **+ Dodaj dysk danych**.</span><span class="sxs-lookup"><span data-stu-id="d795c-154">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="d795c-155">W obszarze **dołączyć istniejącego dysku**, kliknij przycisk **pliku VHD**.</span><span class="sxs-lookup"><span data-stu-id="d795c-155">Under **Attach existing disk**, click **VHD File**.</span></span>
   
   ![Dołączanie istniejącego dysku](./media/attach-disk-portal/attach-existing.png)
3. <span data-ttu-id="d795c-157">W obszarze **kont magazynu**, wybierz konto i kontener, który zawiera plik VHD.</span><span class="sxs-lookup"><span data-stu-id="d795c-157">Under **Storage accounts**, select the account and container that holds the .vhd file.</span></span>
   
   ![Znajdź lokalizację wirtualnego dysku twardego](./media/attach-disk-portal/find-storage-container.png)
4. <span data-ttu-id="d795c-159">Wybierz plik VHD.</span><span class="sxs-lookup"><span data-stu-id="d795c-159">Select the .vhd file.</span></span>
5. <span data-ttu-id="d795c-160">W obszarze **dołączyć istniejącego dysku**, po prostu wybrany plik jest wyświetlana w obszarze **pliku VHD**.</span><span class="sxs-lookup"><span data-stu-id="d795c-160">Under **Attach existing disk**, the file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="d795c-161">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d795c-161">Click **OK**.</span></span>
6. <span data-ttu-id="d795c-162">Po Azure dołącza dysk do maszyny wirtualnej, jest wymienione w ustawieniach dysku maszyny wirtualnej w obszarze **dysków z danymi**.</span><span class="sxs-lookup"><span data-stu-id="d795c-162">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d795c-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d795c-163">Next steps</span></span>
<span data-ttu-id="d795c-164">Po dodaniu dysku, należy przygotować go do użycia.</span><span class="sxs-lookup"><span data-stu-id="d795c-164">After the disk is added, you need to prepare it for use.</span></span> <span data-ttu-id="d795c-165">Aby uzyskać więcej informacji, zobacz [porady: inicjowanie nowy dysk danych w systemie Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="d795c-165">For more information, see [How to: Initialize a new data disk in Linux](add-disk.md).</span></span>
