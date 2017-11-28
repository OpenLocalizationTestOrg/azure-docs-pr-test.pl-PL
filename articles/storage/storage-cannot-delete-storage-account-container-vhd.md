---
title: "Rozwiązywanie problemów z usuwanie konta magazynu platformy Azure, w pojemnikach lub wirtualne dyski twarde w klasycznym wdrożenia | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z usuwanie konta magazynu platformy Azure, w pojemnikach lub wirtualne dyski twarde w wdrożenie klasyczne"
services: storage
documentationcenter: 
author: genlin
manager: felixwu
editor: tysonn
tags: storage
ms.assetid: 0f7a8243-d8dc-432a-9d37-1272a0cb3a5c
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 9f3e824414ad6c1a0aba98a3d549ee63ddc7272f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a><span data-ttu-id="48d9c-103">Rozwiązywanie problemów z usuwanie konta magazynu platformy Azure, w pojemnikach lub wirtualne dyski twarde w wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="48d9c-103">Troubleshoot deleting Azure storage accounts, containers, or VHDs in a classic deployment</span></span>
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

<span data-ttu-id="48d9c-104">Może pojawić się błędy podczas próby usunięcia konta magazynu Azure, kontenera lub dysku VHD w programie [portalu Azure](https://portal.azure.com/) lub [klasycznego portalu Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="48d9c-104">You might receive errors when you try to delete the Azure storage account, container, or VHD in the [Azure portal](https://portal.azure.com/) or the [Azure classic portal](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="48d9c-105">Te problemy mogą być spowodowane przez następujące okoliczności:</span><span class="sxs-lookup"><span data-stu-id="48d9c-105">The issues can be caused by the following circumstances:</span></span>

* <span data-ttu-id="48d9c-106">Dysk i wirtualny dysk twardy nie zostały automatycznie usunięte wraz z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="48d9c-106">When you delete a VM, the disk and VHD are not automatically deleted.</span></span> <span data-ttu-id="48d9c-107">Może to być przyczyną niepowodzenia usuwania konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="48d9c-107">That might be the reason for failure on storage account deletion.</span></span> <span data-ttu-id="48d9c-108">Nie możemy Usuń dysk, dzięki czemu można użyć dysku do zainstalowania inną maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="48d9c-108">We don't delete the disk so that you can use the disk to mount another VM.</span></span>
* <span data-ttu-id="48d9c-109">Nadal istnieje dzierżawa dysku lub obiektu blob skojarzonego z dyskiem.</span><span class="sxs-lookup"><span data-stu-id="48d9c-109">There is still a lease on a disk or the blob that's associated with the disk.</span></span>
* <span data-ttu-id="48d9c-110">Nadal jest obraz maszyny Wirtualnej, który używa konta obiektów blob, kontenera lub magazynu.</span><span class="sxs-lookup"><span data-stu-id="48d9c-110">There is still a VM image that is using a blob, container, or storage account.</span></span>

<span data-ttu-id="48d9c-111">Jeśli problem Azure nie jest opisany w tym artykule, odwiedź fora Azure na [MSDN i przepełnienie stosu](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="48d9c-111">If your Azure issue is not addressed in this article, visit the Azure forums on [MSDN and the Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="48d9c-112">Możesz zamieścić problemu na tych fora lub do @AzureSupport w serwisie Twitter.</span><span class="sxs-lookup"><span data-stu-id="48d9c-112">You can post your issue on these forums or to @AzureSupport on Twitter.</span></span> <span data-ttu-id="48d9c-113">Ponadto można pliku żądania pomocy technicznej platformy Azure, wybierając **uzyskać pomoc techniczną** na [pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) lokacji.</span><span class="sxs-lookup"><span data-stu-id="48d9c-113">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="48d9c-114">Objawy</span><span class="sxs-lookup"><span data-stu-id="48d9c-114">Symptoms</span></span>
<span data-ttu-id="48d9c-115">W poniższej sekcji przedstawiono typowe błędy, które może pojawić się podczas próby usunięcia konta magazynu platformy Azure, kontenery lub wirtualne dyski twarde.</span><span class="sxs-lookup"><span data-stu-id="48d9c-115">The following section lists common errors that you might receive when you try to delete the Azure storage accounts, containers, or VHDs.</span></span>

### <a name="scenario-1-unable-to-delete-a-storage-account"></a><span data-ttu-id="48d9c-116">Scenariusz 1: Nie można usunąć konta magazynu</span><span class="sxs-lookup"><span data-stu-id="48d9c-116">Scenario 1: Unable to delete a storage account</span></span>
<span data-ttu-id="48d9c-117">Po przejściu do konta magazynu classic w [portalu Azure](https://portal.azure.com/) i wybierz **usunąć**, mogą być prezentowane z listy obiektów, które uniemożliwiają usunięcie konta magazynu:</span><span class="sxs-lookup"><span data-stu-id="48d9c-117">When you navigate to the classic storage account in the [Azure portal](https://portal.azure.com/) and select **Delete**, you may be presented with a list of objects that are preventing deletion of the storage account:</span></span>

  ![Obraz błąd podczas usuwania konta magazynu](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

<span data-ttu-id="48d9c-119">Po przejściu do konta magazynu w [klasycznego portalu Azure](https://manage.windowsazure.com/) i wybierz **usunąć**, może pojawić się jeden z następujących błędów:</span><span class="sxs-lookup"><span data-stu-id="48d9c-119">When you navigate to the storage account in the [Azure classic portal](https://manage.windowsazure.com/) and select **Delete**, you might see one of the following errors:</span></span>

- <span data-ttu-id="48d9c-120">*Konto magazynu StorageAccountName zawiera obrazów maszyn wirtualnych. Upewnij się, że te obrazy muszą zostać usunięte przed usunięciem tego konta magazynu.*</span><span class="sxs-lookup"><span data-stu-id="48d9c-120">*Storage account StorageAccountName contains VM Images. Ensure these VM Images are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="48d9c-121">*Nie można usunąć konta magazynu < vm magazynu account-name >. Nie można usunąć konta magazynu < vm magazynu account-name >: "konto magazyn < vm magazynu account-name > ma niektórych aktywne obrazy i/lub dyski. Te obrazy i/lub dyski muszą zostać usunięte przed usunięciem tego konta magazynu. ".*</span><span class="sxs-lookup"><span data-stu-id="48d9c-121">*Failed to delete storage account <vm-storage-account-name>. Unable to delete storage account <vm-storage-account-name>: 'Storage account <vm-storage-account-name> has some active image(s) and/or disk(s). Ensure these image(s) and/or disk(s) are removed before deleting this storage account.'.*</span></span>

- <span data-ttu-id="48d9c-122">*Konto magazynu < vm magazynu account-name > ma niektórych aktywne obrazy i/lub dyski, np. xxxxxxxxx-xxxxxxxxx-O-209490240936090599. Upewnij się, te obrazy i lub dyski muszą zostać usunięte przed usunięciem tego konta magazynu.*</span><span class="sxs-lookup"><span data-stu-id="48d9c-122">*Storage account <vm-storage-account-name> has some active image(s) and/or disk(s), e.g. xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Ensure these image(s) and/or disk(s) are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="48d9c-123">*Konto magazynu < vm magazynu account-name > ma 1 kontenerów, która ma aktywny obraz i/lub artefakty dysku. Te artefakty muszą zostać usunięte z repozytorium obrazów przed usunięciem tego konta magazynu*.</span><span class="sxs-lookup"><span data-stu-id="48d9c-123">*Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from the image repository before deleting this storage account*.</span></span>

- <span data-ttu-id="48d9c-124">*Przedstawia się, że konto magazynu nie powiodła się < vm magazynu account-name > ma 1 kontenerów, która ma aktywny obraz i/lub artefakty dysku. Upewnij się, że te artefakty muszą zostać usunięte z repozytorium obrazów przed usunięciem tego konta magazynu. Podczas próby usunięcia konta magazynu i nie są skojarzone z nim dyski nadal aktywne, zostanie wyświetlony komunikat informujący o active dysków, które muszą zostać usunięte*.</span><span class="sxs-lookup"><span data-stu-id="48d9c-124">*Submit Failed Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from the image repository before deleting this storage account. When you attempt to delete a storage account and there are still active disks associated with it, you will see a message telling you there are active disks that need to be deleted*.</span></span>

### <a name="scenario-2-unable-to-delete-a-container"></a><span data-ttu-id="48d9c-125">Scenariusz 2: Nie można usunąć kontenera</span><span class="sxs-lookup"><span data-stu-id="48d9c-125">Scenario 2: Unable to delete a container</span></span>
<span data-ttu-id="48d9c-126">Podczas próby usunięcia kontenera magazynu, może zostać wyświetlony następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="48d9c-126">When you try to delete the storage container, you might see the following error:</span></span>

<span data-ttu-id="48d9c-127">*Nie można usunąć kontenera magazynu <container name>. Błąd: "jest obecnie dzierżawy w kontenerze i identyfikator dzierżawy nie został określony w żądaniu*.</span><span class="sxs-lookup"><span data-stu-id="48d9c-127">*Failed to delete storage container <container name>. Error: 'There is currently a lease on the container and no lease ID was specified in the request*.</span></span>

<span data-ttu-id="48d9c-128">Lub</span><span class="sxs-lookup"><span data-stu-id="48d9c-128">Or</span></span>

<span data-ttu-id="48d9c-129">*Następujące dyski maszyny wirtualnej korzysta obiekty BLOB w tym kontenerze, dlatego nie można usunąć kontenera: VirtualMachineDiskName1, VirtualMachineDiskName2,...*</span><span class="sxs-lookup"><span data-stu-id="48d9c-129">*The following virtual machine disks use blobs in this container, so the container cannot be deleted: VirtualMachineDiskName1, VirtualMachineDiskName2, ...*</span></span>

### <a name="scenario-3-unable-to-delete-a-vhd"></a><span data-ttu-id="48d9c-130">Scenariusz 3: Nie można usunąć wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="48d9c-130">Scenario 3: Unable to delete a VHD</span></span>
<span data-ttu-id="48d9c-131">Po usunięciu maszyny Wirtualnej i spróbuj go usunąć obiekty BLOB i skojarzone pliki VHD, może pojawić się następujący komunikat:</span><span class="sxs-lookup"><span data-stu-id="48d9c-131">After you delete a VM and then try to delete the blobs for the associated VHDs, you might receive the following message:</span></span>

<span data-ttu-id="48d9c-132">*Nie można usunąć obiektu blob "path/XXXXXX-XXXXXX-os-1447379084699.vhd'. Błąd: "jest obecnie dzierżawy w obiekcie blob i identyfikator dzierżawy nie został określony w żądaniu.*</span><span class="sxs-lookup"><span data-stu-id="48d9c-132">*Failed to delete blob 'path/XXXXXX-XXXXXX-os-1447379084699.vhd'. Error: 'There is currently a lease on the blob and no lease ID was specified in the request.*</span></span>

<span data-ttu-id="48d9c-133">Lub</span><span class="sxs-lookup"><span data-stu-id="48d9c-133">Or</span></span>

<span data-ttu-id="48d9c-134">*Obiektu blob "BlobName.vhd" jest używany jako dysk maszyny wirtualnej "VirtualMachineDiskName", dlatego nie można usunąć obiektu blob.*</span><span class="sxs-lookup"><span data-stu-id="48d9c-134">*Blob 'BlobName.vhd' is in use as virtual machine disk 'VirtualMachineDiskName', so the blob cannot be deleted.*</span></span>

## <a name="solution"></a><span data-ttu-id="48d9c-135">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="48d9c-135">Solution</span></span>
<span data-ttu-id="48d9c-136">Aby rozwiązać najbardziej typowe problemy, wypróbuj następujące metody:</span><span class="sxs-lookup"><span data-stu-id="48d9c-136">To resolve the most common issues, try the following method:</span></span>

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-the-storage-account-container-or-vhd"></a><span data-ttu-id="48d9c-137">Krok 1: Usuń wszystkie dyski, które uniemożliwiają usunięcie konta magazynu, kontenera lub wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="48d9c-137">Step 1: Delete any disks that are preventing deletion of the storage account, container, or VHD</span></span>
1. <span data-ttu-id="48d9c-138">Przełącz się do [klasycznego portalu Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="48d9c-138">Switch to the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="48d9c-139">Wybierz **maszyny WIRTUALNEJ** > **dysków**.</span><span class="sxs-lookup"><span data-stu-id="48d9c-139">Select **VIRTUAL MACHINE** > **DISKS**.</span></span>

    ![Obraz dysków na maszynach wirtualnych w klasycznym portalu Azure.](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. <span data-ttu-id="48d9c-141">Znajdź dyski skojarzone z kontem magazynu, kontenerem lub wirtualnym dyskiem twardym, które chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="48d9c-141">Locate the disks that are associated with the storage account, container, or VHD that you want to delete.</span></span> <span data-ttu-id="48d9c-142">Są one dostępne w lokalizacji dysku.</span><span class="sxs-lookup"><span data-stu-id="48d9c-142">When you check the location of the disk, you will find the associated storage account, container, or VHD.</span></span>

    ![Obraz, który zawiera informacje o lokalizacji dla dysków w klasycznym portalu Azure](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. <span data-ttu-id="48d9c-144">Usuń dyski za pomocą jednej z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="48d9c-144">Delete the disks by using one of the following methods:</span></span>

  - <span data-ttu-id="48d9c-145">Jeśli istnieje maszyna wirtualna nie są wyświetlane na **podłączone do** pola dysku, możesz usunąć dysk bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="48d9c-145">If  there is no VM listed on the **Attached To** field of the disk, you can delete the disk directly.</span></span>

  - <span data-ttu-id="48d9c-146">Jeśli dysk jest dyskiem danych, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="48d9c-146">If the disk is a data disk, follow these steps:</span></span>

    1. <span data-ttu-id="48d9c-147">Sprawdź nazwę dołączonego dysku do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="48d9c-147">Check the name of the VM that the disk is attached to.</span></span>
    2. <span data-ttu-id="48d9c-148">Przejdź do **maszyn wirtualnych** > **wystąpień**, a następnie zlokalizuj maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="48d9c-148">Go to **Virtual Machines** > **Instances**, and then locate the VM.</span></span>
    3. <span data-ttu-id="48d9c-149">Upewnij się, że nic nie jest aktywnie przy użyciu dysku.</span><span class="sxs-lookup"><span data-stu-id="48d9c-149">Make sure that nothing is actively using the disk.</span></span>
    4. <span data-ttu-id="48d9c-150">Wybierz **odłączyć dysku** w dolnej części portalu, aby odłączyć dysk.</span><span class="sxs-lookup"><span data-stu-id="48d9c-150">Select **Detach Disk** at the bottom of the portal to detach the disk.</span></span>
    5. <span data-ttu-id="48d9c-151">Przejdź do **maszyn wirtualnych** > **dysków**i zaczekaj, aż **podłączone do** pola, aby włączyć puste.</span><span class="sxs-lookup"><span data-stu-id="48d9c-151">Go to **Virtual Machines** > **Disks**, and wait for the **Attached To** field to turn blank.</span></span> <span data-ttu-id="48d9c-152">Oznacza to, że dysk został pomyślnie odłączona od maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="48d9c-152">This indicates the disk has successfully detached from the VM.</span></span>
    6. <span data-ttu-id="48d9c-153">Wybierz **usunąć** w dolnej części **maszyn wirtualnych** > **dysków** można usunąć dysku.</span><span class="sxs-lookup"><span data-stu-id="48d9c-153">Select **Delete** at the bottom of **Virtual Machines** > **Disks** to delete the disk.</span></span>

  - <span data-ttu-id="48d9c-154">Jeśli dysk jest dyskiem systemu operacyjnego ( **zawiera system operacyjny** pole ma wartość, takich jak system Windows) i dołączony do maszyny Wirtualnej, wykonaj następujące kroki, aby usunąć maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="48d9c-154">If the disk is an OS disk (the **Contains OS** field has a value like Windows) and attached to a VM, follow these steps to delete the VM.</span></span> <span data-ttu-id="48d9c-155">Nie można odłączyć dysk systemu operacyjnego, a więc musimy usunąć maszynę Wirtualną do zwolnienia dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="48d9c-155">The OS disk cannot be detached, so we have to delete the VM to release the lease.</span></span>

    1. <span data-ttu-id="48d9c-156">Sprawdź nazwę dysk danych jest dołączony do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="48d9c-156">Check the name of the Virtual Machine the Data Disk is attached to.</span></span>  
    2. <span data-ttu-id="48d9c-157">Przejdź do **maszyn wirtualnych** > **wystąpień**, a następnie wybierz dysk dołączony do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="48d9c-157">Go to **Virtual Machines** > **Instances**, and then select the VM that the disk is attached to.</span></span>
    3. <span data-ttu-id="48d9c-158">Upewnij się, że nic nie jest aktywnie przy użyciu maszyny wirtualnej i nie są już potrzebne maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="48d9c-158">Make sure that nothing is actively using the virtual machine, and that you no longer need the virtual machine.</span></span>
    4. <span data-ttu-id="48d9c-159">Wybierz dysk maszyny Wirtualnej jest dołączony do, następnie wybierz **usunąć** > **usuwanie dołączonych dysków**.</span><span class="sxs-lookup"><span data-stu-id="48d9c-159">Select the VM the disk is attached to, then select **Delete** > **Delete the attached disks**.</span></span>
    5. <span data-ttu-id="48d9c-160">Przejdź do **maszyn wirtualnych** > **dysków**i zaczekaj na znikają dysku.</span><span class="sxs-lookup"><span data-stu-id="48d9c-160">Go to **Virtual Machines** > **Disks**, and wait for the disk to disappear.</span></span>  <span data-ttu-id="48d9c-161">Może upłynąć kilka minut, aż to możliwe, i może być konieczne odświeżenie strony.</span><span class="sxs-lookup"><span data-stu-id="48d9c-161">It may take a few minutes for this to occur, and you may need to refresh the page.</span></span>
    6. <span data-ttu-id="48d9c-162">Jeśli dysk nie zniknie, poczekaj, aż **podłączone do** pola, aby włączyć puste.</span><span class="sxs-lookup"><span data-stu-id="48d9c-162">If the disk does not disappear, wait for the **Attached To** field to turn blank.</span></span> <span data-ttu-id="48d9c-163">Oznacza to, że dysk pełni została odłączona od maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="48d9c-163">This indicates the disk has fully detached from the VM.</span></span>  <span data-ttu-id="48d9c-164">Następnie wybierz dysk i wybierz **usunąć** w dolnej części strony, aby usunąć dysk.</span><span class="sxs-lookup"><span data-stu-id="48d9c-164">Then, select the disk, and select **Delete** at the bottom of the page to delete the disk.</span></span>


   > [!NOTE]
   > <span data-ttu-id="48d9c-165">Jeśli dysk jest dołączony do maszyny Wirtualnej, nie można go usunąć.</span><span class="sxs-lookup"><span data-stu-id="48d9c-165">If a disk is attached to a VM, you will not be able to delete it.</span></span> <span data-ttu-id="48d9c-166">Dyski są odłączone asynchronicznie z usuniętych maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="48d9c-166">Disks are detached from a deleted VM asynchronously.</span></span> <span data-ttu-id="48d9c-167">Może upłynąć kilka minut, po usunięciu maszyny Wirtualnej dla tego pola wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="48d9c-167">It might take a few minutes after the VM is deleted for this field to clear up.</span></span>
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-the-storage-account-or-container"></a><span data-ttu-id="48d9c-168">Krok 2: Usuń wszelkie obrazy maszyny Wirtualnej, które uniemożliwiają usunięcie konta magazynu i kontener</span><span class="sxs-lookup"><span data-stu-id="48d9c-168">Step 2: Delete any VM Images that are preventing deletion of the storage account or container</span></span>
1. <span data-ttu-id="48d9c-169">Przełącz się do [klasycznego portalu Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="48d9c-169">Switch to the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="48d9c-170">Wybierz **maszyny WIRTUALNEJ** > **obrazów**, a następnie usuń obrazów, które są skojarzone z kontem magazynu, kontenera lub wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="48d9c-170">Select **VIRTUAL MACHINE** > **IMAGES**, and then delete the images that are associated with the storage account, container, or VHD.</span></span>

    <span data-ttu-id="48d9c-171">Następnie ponownie spróbuj usunąć konto magazynu, kontenera lub wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="48d9c-171">After that, try to delete the storage account, container, or VHD again.</span></span>

> [!WARNING]
> <span data-ttu-id="48d9c-172">Zanim usuniesz konto, wykonaj kopię zapasową wszystkich danych, które chcesz zapisać.</span><span class="sxs-lookup"><span data-stu-id="48d9c-172">Be sure to back up anything you want to save before you delete the account.</span></span> <span data-ttu-id="48d9c-173">Po usunięciu wirtualnego dysku twardego, obiektów blob, tabeli, kolejki lub pliku spowoduje jego trwałe skasowanie.</span><span class="sxs-lookup"><span data-stu-id="48d9c-173">Once you delete a VHD, blob, table, queue, or file, it is permanently deleted.</span></span> <span data-ttu-id="48d9c-174">Upewnij się, że zasób nie jest w użyciu.</span><span class="sxs-lookup"><span data-stu-id="48d9c-174">Ensure that the resource is not in use.</span></span>
>
>

## <a name="about-the-stopped-deallocated-status"></a><span data-ttu-id="48d9c-175">Stan zatrzymane (cofnięciu przydziału)</span><span class="sxs-lookup"><span data-stu-id="48d9c-175">About the Stopped (deallocated) status</span></span>
<span data-ttu-id="48d9c-176">Maszyny wirtualne, które zostały utworzone w klasycznym modelu wdrażania i zostać zatrzymane będą miały **zatrzymane (cofnięciu przydziału)** stanu w zależności [portalu Azure](https://portal.azure.com/) lub [klasycznego portalu Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="48d9c-176">VMs that were created in the classic deployment model and that have been retained will have the **Stopped (deallocated)** status on either the [Azure portal](https://portal.azure.com/) or [Azure classic portal](https://manage.windowsazure.com/).</span></span>

<span data-ttu-id="48d9c-177">**Klasyczny portal Azure**:</span><span class="sxs-lookup"><span data-stu-id="48d9c-177">**Azure classic portal**:</span></span>

![Zatrzymano stanu (Deallocated) dla maszyn wirtualnych z portalu Azure.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

<span data-ttu-id="48d9c-179">**Azure portal**:</span><span class="sxs-lookup"><span data-stu-id="48d9c-179">**Azure portal**:</span></span>

![Zatrzymana (cofnięciu przydziału) stanu dla maszyn wirtualnych w klasycznym portalu Azure.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

<span data-ttu-id="48d9c-181">Stan "Zatrzymane (cofnięciu przydziału)" zwalnia zasoby komputera, na przykład procesora CPU, pamięci i sieci.</span><span class="sxs-lookup"><span data-stu-id="48d9c-181">A "Stopped (deallocated)" status releases the computer resources, such as the CPU, memory, and network.</span></span> <span data-ttu-id="48d9c-182">Dyski, jednak są nadal przechowywane, dzięki czemu będzie można szybko utworzyć ponownie maszynę Wirtualną w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="48d9c-182">The disks, however, are still retained so that you can quickly re-create the VM if necessary.</span></span> <span data-ttu-id="48d9c-183">Te dyski są tworzone na wirtualne dyski twarde, które bazują na magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="48d9c-183">These disks are created on top of VHDs, which are backed by Azure storage.</span></span> <span data-ttu-id="48d9c-184">Konto magazynu ma następujące wirtualne dyski twarde, a dyski mają dzierżawy na tych dyskach VHD.</span><span class="sxs-lookup"><span data-stu-id="48d9c-184">The storage account has these VHDs, and the disks have leases on those VHDs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48d9c-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="48d9c-185">Next steps</span></span>
* [<span data-ttu-id="48d9c-186">Usunięcie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="48d9c-186">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
