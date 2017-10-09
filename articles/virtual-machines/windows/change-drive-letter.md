---
title: "Upewnij się, hello dysku D: dysku danych maszyny wirtualnej | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toochange litery dysków dla maszyny Wirtualnej systemu Windows tak, aby można było używać dysków D: hello jako dysk danych."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 0867a931-0055-4e31-8403-9b38a3eeb904
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: cynthn
ms.openlocfilehash: 43939da1a890ac4049266487951e3889aa0ed9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-d-drive-as-a-data-drive-on-a-windows-vm"></a><span data-ttu-id="076f3-103">Użyj dysku D: hello jako dysk z danymi na maszynie Wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="076f3-103">Use hello D: drive as a data drive on a Windows VM</span></span>
<span data-ttu-id="076f3-104">Jeśli aplikacja wymaga hello toouse danych toostore dysku D, wykonaj te instrukcje toouse inną literę dysku tymczasowym hello.</span><span class="sxs-lookup"><span data-stu-id="076f3-104">If your application needs toouse hello D drive toostore data, follow these instructions toouse a different drive letter for hello temporary disk.</span></span> <span data-ttu-id="076f3-105">Nigdy nie używaj danych toostore dysku tymczasowym hello konieczność tookeep.</span><span class="sxs-lookup"><span data-stu-id="076f3-105">Never use hello temporary disk toostore data that you need tookeep.</span></span>

<span data-ttu-id="076f3-106">Jeśli po zmianie rozmiaru lub **Stop (Deallocate)** maszyny wirtualnej, może to wywołać umieszczania nowej funkcji hypervisor hello maszyn wirtualnych tooa.</span><span class="sxs-lookup"><span data-stu-id="076f3-106">If you resize or **Stop (Deallocate)** a virtual machine, this may trigger placement of hello virtual machine tooa new hypervisor.</span></span> <span data-ttu-id="076f3-107">Planowanego lub nieplanowanego zdarzenia konserwacji może być również przyczyną tego rozmieszczenia.</span><span class="sxs-lookup"><span data-stu-id="076f3-107">A planned or unplanned maintenance event may also trigger this placement.</span></span> <span data-ttu-id="076f3-108">W tym scenariuszu dysku tymczasowym hello będzie przypisywać ich toohello pierwszą dostępną literę dysku.</span><span class="sxs-lookup"><span data-stu-id="076f3-108">In this scenario, hello temporary disk will be reassigned toohello first available drive letter.</span></span> <span data-ttu-id="076f3-109">Jeśli masz aplikację, która wymaga specjalnie hello D: dysku, należy toofollow, te kroki tootemporarily przenoszenia hello pagefile.sys dołączyć nowego dysku danych i przypisać jej literę hello D, a następnie przenieś hello pagefile.sys kopii toohello tymczasowej stacji.</span><span class="sxs-lookup"><span data-stu-id="076f3-109">If you have an application that specifically requires hello D: drive, you need toofollow these steps tootemporarily move hello pagefile.sys, attach a new data disk and assign it hello letter D and then move hello pagefile.sys back toohello temporary drive.</span></span> <span data-ttu-id="076f3-110">Po wykonaniu tych czynności Azure nie wycofania hello D: Jeśli hello maszyna wirtualna zostanie przeniesiona tooa innej funkcji hypervisor.</span><span class="sxs-lookup"><span data-stu-id="076f3-110">Once complete, Azure will not take back hello D: if hello VM moves tooa different hypervisor.</span></span>

<span data-ttu-id="076f3-111">Aby uzyskać więcej informacji o używaniu dysku tymczasowym hello Azure, zobacz [opis hello tymczasowej stacji na maszynach wirtualnych Azure firmy Microsoft](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="076f3-111">For more information about how Azure uses hello temporary disk, see [Understanding hello temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>

## <a name="attach-hello-data-disk"></a><span data-ttu-id="076f3-112">Dołączenie dysku danych hello</span><span class="sxs-lookup"><span data-stu-id="076f3-112">Attach hello data disk</span></span>
<span data-ttu-id="076f3-113">Najpierw należy maszyny wirtualnej toohello tooattach hello dane dysku.</span><span class="sxs-lookup"><span data-stu-id="076f3-113">First, you'll need tooattach hello data disk toohello virtual machine.</span></span> <span data-ttu-id="076f3-114">toodo to przy użyciu portalu hello, zobacz [jak tooattach zarządzanych danych na dysku w portalu Azure hello](attach-managed-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="076f3-114">toodo this using hello portal, see [How tooattach a managed data disk in hello Azure portal](attach-managed-disk-portal.md).</span></span>

## <a name="temporarily-move-pagefilesys-tooc-drive"></a><span data-ttu-id="076f3-115">Tymczasowo przenieść pagefile.sys tooC dysku</span><span class="sxs-lookup"><span data-stu-id="076f3-115">Temporarily move pagefile.sys tooC drive</span></span>
1. <span data-ttu-id="076f3-116">Połącz toohello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="076f3-116">Connect toohello virtual machine.</span></span> 
2. <span data-ttu-id="076f3-117">Kliknij prawym przyciskiem myszy hello **Start** menu i wybierz **systemu**.</span><span class="sxs-lookup"><span data-stu-id="076f3-117">Right-click hello **Start** menu and select **System**.</span></span>
3. <span data-ttu-id="076f3-118">W menu po lewej stronie powitania, wybierz **Zaawansowane ustawienia systemu**.</span><span class="sxs-lookup"><span data-stu-id="076f3-118">In hello left-hand menu, select **Advanced system settings**.</span></span>
4. <span data-ttu-id="076f3-119">W hello **wydajności** zaznacz **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="076f3-119">In hello **Performance** section, select **Settings**.</span></span>
5. <span data-ttu-id="076f3-120">Wybierz hello **zaawansowane** kartę.</span><span class="sxs-lookup"><span data-stu-id="076f3-120">Select hello **Advanced** tab.</span></span>
6. <span data-ttu-id="076f3-121">W hello **pamięci wirtualnej** zaznacz **zmiany**.</span><span class="sxs-lookup"><span data-stu-id="076f3-121">In hello **Virtual memory** section, select **Change**.</span></span>
7. <span data-ttu-id="076f3-122">Wybierz hello **C** dysk, a następnie kliknij przycisk **Rozmiar kontrolowany przez System** , a następnie kliknij przycisk **ustawić**.</span><span class="sxs-lookup"><span data-stu-id="076f3-122">Select hello **C** drive and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="076f3-123">Wybierz hello **D** dysk, a następnie kliknij przycisk **plik stronicowania nie** , a następnie kliknij przycisk **ustawić**.</span><span class="sxs-lookup"><span data-stu-id="076f3-123">Select hello **D** drive and then click **No paging file** and then click **Set**.</span></span>
9. <span data-ttu-id="076f3-124">Kliknij przycisk Zastosuj.</span><span class="sxs-lookup"><span data-stu-id="076f3-124">Click Apply.</span></span> <span data-ttu-id="076f3-125">Zostanie wyświetlone ostrzeżenie komputera hello musi toobe hello zmiany tootake mają wpływ na ponowne uruchomienie.</span><span class="sxs-lookup"><span data-stu-id="076f3-125">You will get a warning that hello computer needs toobe restarted for hello changes tootake affect.</span></span>
10. <span data-ttu-id="076f3-126">Uruchom ponownie maszynę wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="076f3-126">Restart hello virtual machine.</span></span>

## <a name="change-hello-drive-letters"></a><span data-ttu-id="076f3-127">Zmień litery dysków hello</span><span class="sxs-lookup"><span data-stu-id="076f3-127">Change hello drive letters</span></span>
1. <span data-ttu-id="076f3-128">Raz hello ponownego uruchomienia maszyny Wirtualnej, zaloguj się ponownie toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="076f3-128">Once hello VM restarts, log back on toohello VM.</span></span>
2. <span data-ttu-id="076f3-129">Kliknij przycisk hello **Start** menu i typ **diskmgmt.msc** i naciśnij Enter.</span><span class="sxs-lookup"><span data-stu-id="076f3-129">Click hello **Start** menu and type **diskmgmt.msc** and hit Enter.</span></span> <span data-ttu-id="076f3-130">Rozpocznie się Zarządzanie dyskami.</span><span class="sxs-lookup"><span data-stu-id="076f3-130">Disk Management will start.</span></span>
3. <span data-ttu-id="076f3-131">Kliknij prawym przyciskiem myszy **D**hello magazyn tymczasowy dysku i wybierz **Zmień literę dysku i ścieżki**.</span><span class="sxs-lookup"><span data-stu-id="076f3-131">Right-click on **D**, hello Temporary Storage drive, and select **Change Drive Letter and Paths**.</span></span>
4. <span data-ttu-id="076f3-132">W obszarze literę dysku, wybierz inny dysk takich jak **T** , a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="076f3-132">Under Drive letter, select a new drive such as **T** and then click **OK**.</span></span> 
5. <span data-ttu-id="076f3-133">Kliknij prawym przyciskiem myszy na powitania dysku danych, a następnie wybierz **Zmień literę dysku i ścieżki**.</span><span class="sxs-lookup"><span data-stu-id="076f3-133">Right-click on hello data disk, and select **Change Drive Letter and Paths**.</span></span>
6. <span data-ttu-id="076f3-134">W obszarze literę dysku, należy wybrać dysk **D** , a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="076f3-134">Under Drive letter, select drive **D** and then click **OK**.</span></span> 

## <a name="move-pagefilesys-back-toohello-temporary-storage-drive"></a><span data-ttu-id="076f3-135">Przenieś pagefile.sys wstecz toohello magazyn tymczasowy dysku</span><span class="sxs-lookup"><span data-stu-id="076f3-135">Move pagefile.sys back toohello temporary storage drive</span></span>
1. <span data-ttu-id="076f3-136">Kliknij prawym przyciskiem myszy hello **Start** menu i wybierz **systemu**</span><span class="sxs-lookup"><span data-stu-id="076f3-136">Right-click hello **Start** menu and select **System**</span></span>
2. <span data-ttu-id="076f3-137">W menu po lewej stronie powitania, wybierz **Zaawansowane ustawienia systemu**.</span><span class="sxs-lookup"><span data-stu-id="076f3-137">In hello left-hand menu, select **Advanced system settings**.</span></span>
3. <span data-ttu-id="076f3-138">W hello **wydajności** zaznacz **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="076f3-138">In hello **Performance** section, select **Settings**.</span></span>
4. <span data-ttu-id="076f3-139">Wybierz hello **zaawansowane** kartę.</span><span class="sxs-lookup"><span data-stu-id="076f3-139">Select hello **Advanced** tab.</span></span>
5. <span data-ttu-id="076f3-140">W hello **pamięci wirtualnej** zaznacz **zmiany**.</span><span class="sxs-lookup"><span data-stu-id="076f3-140">In hello **Virtual memory** section, select **Change**.</span></span>
6. <span data-ttu-id="076f3-141">Wybierz dysk systemu operacyjnego hello **C** i kliknij przycisk **plik stronicowania nie** , a następnie kliknij przycisk **ustawić**.</span><span class="sxs-lookup"><span data-stu-id="076f3-141">Select hello OS drive **C** and click **No paging file** and then click **Set**.</span></span>
7. <span data-ttu-id="076f3-142">Wybierz dysk magazyn tymczasowy hello **T** , a następnie kliknij przycisk **Rozmiar kontrolowany przez System** , a następnie kliknij przycisk **ustawić**.</span><span class="sxs-lookup"><span data-stu-id="076f3-142">Select hello temporary storage drive **T** and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="076f3-143">Kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="076f3-143">Click **Apply**.</span></span> <span data-ttu-id="076f3-144">Zostanie wyświetlone ostrzeżenie komputera hello musi toobe hello zmiany tootake mają wpływ na ponowne uruchomienie.</span><span class="sxs-lookup"><span data-stu-id="076f3-144">You will get a warning that hello computer needs toobe restarted for hello changes tootake affect.</span></span>
9. <span data-ttu-id="076f3-145">Uruchom ponownie maszynę wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="076f3-145">Restart hello virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="076f3-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="076f3-146">Next steps</span></span>
* <span data-ttu-id="076f3-147">Można zwiększyć maszyny wirtualnej dostępne tooyour hello magazynu za pomocą [dołączenie dysku danych dodatkowych](attach-managed-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="076f3-147">You can increase hello storage available tooyour virtual machine by [attaching a additional data disk](attach-managed-disk-portal.md).</span></span>

