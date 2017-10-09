---
title: "aaaTroubleshoot usuwanie konta magazynu platformy Azure, w pojemnikach lub wirtualne dyski twarde w klasycznym wdrożenia | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 6bbfa032e1968718c623227bb426d553e2951075
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a><span data-ttu-id="e48ef-103">Rozwiązywanie problemów z usuwanie konta magazynu platformy Azure, w pojemnikach lub wirtualne dyski twarde w wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="e48ef-103">Troubleshoot deleting Azure storage accounts, containers, or VHDs in a classic deployment</span></span>
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

<span data-ttu-id="e48ef-104">Może pojawić się błędy podczas próby toodelete hello konta magazynu Azure, kontenera lub wirtualnego dysku twardego w hello [portalu Azure](https://portal.azure.com/) lub hello [klasycznego portalu Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="e48ef-104">You might receive errors when you try toodelete hello Azure storage account, container, or VHD in hello [Azure portal](https://portal.azure.com/) or hello [Azure classic portal](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="e48ef-105">Witaj problemów może być spowodowane hello w następujących okolicznościach:</span><span class="sxs-lookup"><span data-stu-id="e48ef-105">hello issues can be caused by hello following circumstances:</span></span>

* <span data-ttu-id="e48ef-106">Po usunięciu maszyny Wirtualnej hello dysku i wirtualnego dysku twardego nie są automatycznie usuwane.</span><span class="sxs-lookup"><span data-stu-id="e48ef-106">When you delete a VM, hello disk and VHD are not automatically deleted.</span></span> <span data-ttu-id="e48ef-107">Może to być hello Przyczyna niepowodzenia usuwania konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="e48ef-107">That might be hello reason for failure on storage account deletion.</span></span> <span data-ttu-id="e48ef-108">Firma Microsoft nie należy usuwać hello dysku, aby mogli używać toomount dysku hello inną maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="e48ef-108">We don't delete hello disk so that you can use hello disk toomount another VM.</span></span>
* <span data-ttu-id="e48ef-109">Na dysku lub hello obiektu blob skojarzoną z dyskiem hello nadal jest dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="e48ef-109">There is still a lease on a disk or hello blob that's associated with hello disk.</span></span>
* <span data-ttu-id="e48ef-110">Nadal jest obraz maszyny Wirtualnej, który używa konta obiektów blob, kontenera lub magazynu.</span><span class="sxs-lookup"><span data-stu-id="e48ef-110">There is still a VM image that is using a blob, container, or storage account.</span></span>

<span data-ttu-id="e48ef-111">Jeśli problem Azure nie jest opisany w tym artykule, odwiedź hello na forach platformy Azure [MSDN i hello przepełnienie stosu](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="e48ef-111">If your Azure issue is not addressed in this article, visit hello Azure forums on [MSDN and hello Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="e48ef-112">Problem można umieścić na tych fora lub too@AzureSupport w serwisie Twitter.</span><span class="sxs-lookup"><span data-stu-id="e48ef-112">You can post your issue on these forums or too@AzureSupport on Twitter.</span></span> <span data-ttu-id="e48ef-113">Ponadto można pliku żądania pomocy technicznej platformy Azure, wybierając **uzyskać pomoc techniczną** na powitania [pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) lokacji.</span><span class="sxs-lookup"><span data-stu-id="e48ef-113">Also, you can file an Azure support request by selecting **Get support** on hello [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="e48ef-114">Objawy</span><span class="sxs-lookup"><span data-stu-id="e48ef-114">Symptoms</span></span>
<span data-ttu-id="e48ef-115">powitania po sekcja zawiera listę typowych błędów, które może pojawić się podczas próby kontami magazynu Azure hello toodelete, kontenery lub wirtualne dyski twarde.</span><span class="sxs-lookup"><span data-stu-id="e48ef-115">hello following section lists common errors that you might receive when you try toodelete hello Azure storage accounts, containers, or VHDs.</span></span>

### <a name="scenario-1-unable-toodelete-a-storage-account"></a><span data-ttu-id="e48ef-116">Scenariusz 1: Nie można toodelete konta magazynu</span><span class="sxs-lookup"><span data-stu-id="e48ef-116">Scenario 1: Unable toodelete a storage account</span></span>
<span data-ttu-id="e48ef-117">Po przejściu konta magazynu classic toohello w hello [portalu Azure](https://portal.azure.com/) i wybierz **usunąć**, mogą być prezentowane z listy obiektów, które uniemożliwiają usunięcie konta magazynu hello:</span><span class="sxs-lookup"><span data-stu-id="e48ef-117">When you navigate toohello classic storage account in hello [Azure portal](https://portal.azure.com/) and select **Delete**, you may be presented with a list of objects that are preventing deletion of hello storage account:</span></span>

  ![Obraz błąd podczas usuwania konta magazynu hello](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

<span data-ttu-id="e48ef-119">Po przejściu toohello konta magazynu w hello [klasycznego portalu Azure](https://manage.windowsazure.com/) i wybierz **usunąć**, może pojawić się jeden hello następujące błędy:</span><span class="sxs-lookup"><span data-stu-id="e48ef-119">When you navigate toohello storage account in hello [Azure classic portal](https://manage.windowsazure.com/) and select **Delete**, you might see one of hello following errors:</span></span>

- <span data-ttu-id="e48ef-120">*Konto magazynu StorageAccountName zawiera obrazów maszyn wirtualnych. Upewnij się, że te obrazy muszą zostać usunięte przed usunięciem tego konta magazynu.*</span><span class="sxs-lookup"><span data-stu-id="e48ef-120">*Storage account StorageAccountName contains VM Images. Ensure these VM Images are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="e48ef-121">*Konto magazynu toodelete < vm magazynu account-name > nie powiodło się. Konto magazynu toodelete < vm magazynu account-name >: "konto magazyn < vm magazynu account-name > ma niektórych aktywne obrazy i/lub dyski. Te obrazy i/lub dyski muszą zostać usunięte przed usunięciem tego konta magazynu. ".*</span><span class="sxs-lookup"><span data-stu-id="e48ef-121">*Failed toodelete storage account <vm-storage-account-name>. Unable toodelete storage account <vm-storage-account-name>: 'Storage account <vm-storage-account-name> has some active image(s) and/or disk(s). Ensure these image(s) and/or disk(s) are removed before deleting this storage account.'.*</span></span>

- <span data-ttu-id="e48ef-122">*Konto magazynu < vm magazynu account-name > ma niektórych aktywne obrazy i/lub dyski, np. xxxxxxxxx-xxxxxxxxx-O-209490240936090599. Upewnij się, te obrazy i lub dyski muszą zostać usunięte przed usunięciem tego konta magazynu.*</span><span class="sxs-lookup"><span data-stu-id="e48ef-122">*Storage account <vm-storage-account-name> has some active image(s) and/or disk(s), e.g. xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Ensure these image(s) and/or disk(s) are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="e48ef-123">*Konto magazynu < vm magazynu account-name > ma 1 kontenerów, która ma aktywny obraz i/lub artefakty dysku. Te artefakty muszą zostać usunięte z repozytorium obrazów hello przed usunięciem tego konta magazynu*.</span><span class="sxs-lookup"><span data-stu-id="e48ef-123">*Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from hello image repository before deleting this storage account*.</span></span>

- <span data-ttu-id="e48ef-124">*Przedstawia się, że konto magazynu nie powiodła się < vm magazynu account-name > ma 1 kontenerów, która ma aktywny obraz i/lub artefakty dysku. Upewnij się, że te artefakty muszą zostać usunięte z repozytorium obrazów hello przed usunięciem tego konta magazynu. Podczas próby toodelete konta magazynu i nie są skojarzone z nim dyski nadal aktywne, zostanie wyświetlony komunikat informujący o tym, istnieją aktywne dysków, które należy usunąć toobe*.</span><span class="sxs-lookup"><span data-stu-id="e48ef-124">*Submit Failed Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from hello image repository before deleting this storage account. When you attempt toodelete a storage account and there are still active disks associated with it, you will see a message telling you there are active disks that need toobe deleted*.</span></span>

### <a name="scenario-2-unable-toodelete-a-container"></a><span data-ttu-id="e48ef-125">Scenariusz 2: Nie można toodelete kontenera</span><span class="sxs-lookup"><span data-stu-id="e48ef-125">Scenario 2: Unable toodelete a container</span></span>
<span data-ttu-id="e48ef-126">Podczas próby kontenera magazynu hello toodelete można napotkać hello następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="e48ef-126">When you try toodelete hello storage container, you might see hello following error:</span></span>

<span data-ttu-id="e48ef-127">*Kontenera magazynu nie powiodło się toodelete <container name>. Błąd: "jest obecnie dzierżawy w kontenerze hello i identyfikator dzierżawy nie został określony w żądaniu hello*.</span><span class="sxs-lookup"><span data-stu-id="e48ef-127">*Failed toodelete storage container <container name>. Error: 'There is currently a lease on hello container and no lease ID was specified in hello request*.</span></span>

<span data-ttu-id="e48ef-128">Lub</span><span class="sxs-lookup"><span data-stu-id="e48ef-128">Or</span></span>

<span data-ttu-id="e48ef-129">*powitania po dysków maszyny wirtualnej korzysta obiekty BLOB w tym kontenerze, dlatego nie można usunąć kontenera hello: VirtualMachineDiskName1, VirtualMachineDiskName2,...*</span><span class="sxs-lookup"><span data-stu-id="e48ef-129">*hello following virtual machine disks use blobs in this container, so hello container cannot be deleted: VirtualMachineDiskName1, VirtualMachineDiskName2, ...*</span></span>

### <a name="scenario-3-unable-toodelete-a-vhd"></a><span data-ttu-id="e48ef-130">Scenariusz 3: Nie można toodelete wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="e48ef-130">Scenario 3: Unable toodelete a VHD</span></span>
<span data-ttu-id="e48ef-131">Po usunięciu maszyny Wirtualnej i następnie obiekty BLOB hello toodelete spróbuj dla hello odpowiednich wirtualne dyski twarde, może pojawić się następujące wiadomość hello:</span><span class="sxs-lookup"><span data-stu-id="e48ef-131">After you delete a VM and then try toodelete hello blobs for hello associated VHDs, you might receive hello following message:</span></span>

<span data-ttu-id="e48ef-132">*Obiekt blob toodelete nie powiodło się "path/XXXXXX-XXXXXX-os-1447379084699.vhd'. Błąd: "jest obecnie dzierżawy na powitania obiektów blob i identyfikator dzierżawy nie został określony w żądaniu hello.*</span><span class="sxs-lookup"><span data-stu-id="e48ef-132">*Failed toodelete blob 'path/XXXXXX-XXXXXX-os-1447379084699.vhd'. Error: 'There is currently a lease on hello blob and no lease ID was specified in hello request.*</span></span>

<span data-ttu-id="e48ef-133">Lub</span><span class="sxs-lookup"><span data-stu-id="e48ef-133">Or</span></span>

<span data-ttu-id="e48ef-134">*Obiektu blob "BlobName.vhd" jest używany jako dysk maszyny wirtualnej "VirtualMachineDiskName", dlatego nie można usunąć obiektu blob hello.*</span><span class="sxs-lookup"><span data-stu-id="e48ef-134">*Blob 'BlobName.vhd' is in use as virtual machine disk 'VirtualMachineDiskName', so hello blob cannot be deleted.*</span></span>

## <a name="solution"></a><span data-ttu-id="e48ef-135">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="e48ef-135">Solution</span></span>
<span data-ttu-id="e48ef-136">tooresolve hello najbardziej typowe problemy, spróbuj hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="e48ef-136">tooresolve hello most common issues, try hello following method:</span></span>

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-hello-storage-account-container-or-vhd"></a><span data-ttu-id="e48ef-137">Krok 1: Usuń wszystkie dyski, które uniemożliwiają usunięcie konta magazynu hello, kontenera lub wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="e48ef-137">Step 1: Delete any disks that are preventing deletion of hello storage account, container, or VHD</span></span>
1. <span data-ttu-id="e48ef-138">Przełącz toohello [klasycznego portalu Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="e48ef-138">Switch toohello [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="e48ef-139">Wybierz **maszyny WIRTUALNEJ** > **dysków**.</span><span class="sxs-lookup"><span data-stu-id="e48ef-139">Select **VIRTUAL MACHINE** > **DISKS**.</span></span>

    ![Obraz dysków na maszynach wirtualnych w klasycznym portalu Azure.](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. <span data-ttu-id="e48ef-141">Zlokalizuj hello dysków, które są skojarzone z konta magazynu hello, kontenera lub dysku VHD, które mają toodelete.</span><span class="sxs-lookup"><span data-stu-id="e48ef-141">Locate hello disks that are associated with hello storage account, container, or VHD that you want toodelete.</span></span> <span data-ttu-id="e48ef-142">Po zaznaczeniu hello lokalizację dysku hello znajdziesz hello skojarzonego konta magazynu, kontenera lub wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="e48ef-142">When you check hello location of hello disk, you will find hello associated storage account, container, or VHD.</span></span>

    ![Obraz, który zawiera informacje o lokalizacji dla dysków w klasycznym portalu Azure](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. <span data-ttu-id="e48ef-144">Usuń dyski hello przy użyciu jednej z następujących metod hello:</span><span class="sxs-lookup"><span data-stu-id="e48ef-144">Delete hello disks by using one of hello following methods:</span></span>

  - <span data-ttu-id="e48ef-145">Jeśli istnieje maszyna wirtualna nie są wyświetlane na hello **podłączone do** pola hello dysku, możesz usunąć dysk hello bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="e48ef-145">If  there is no VM listed on hello **Attached To** field of hello disk, you can delete hello disk directly.</span></span>

  - <span data-ttu-id="e48ef-146">Jeśli dysk hello jest dysk danych, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e48ef-146">If hello disk is a data disk, follow these steps:</span></span>

    1. <span data-ttu-id="e48ef-147">Sprawdź nazwę hello hello, w której jest dołączona maszyna wirtualna, która hello dysku.</span><span class="sxs-lookup"><span data-stu-id="e48ef-147">Check hello name of hello VM that hello disk is attached to.</span></span>
    2. <span data-ttu-id="e48ef-148">Przejdź za**maszyn wirtualnych** > **wystąpień**, a następnie zlokalizuj hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e48ef-148">Go too**Virtual Machines** > **Instances**, and then locate hello VM.</span></span>
    3. <span data-ttu-id="e48ef-149">Upewnij się, że nic nie jest aktywnie używających hello dysku.</span><span class="sxs-lookup"><span data-stu-id="e48ef-149">Make sure that nothing is actively using hello disk.</span></span>
    4. <span data-ttu-id="e48ef-150">Wybierz **odłączyć dysku** u dołu hello hello portalu toodetach hello dysku.</span><span class="sxs-lookup"><span data-stu-id="e48ef-150">Select **Detach Disk** at hello bottom of hello portal toodetach hello disk.</span></span>
    5. <span data-ttu-id="e48ef-151">Przejdź za**maszyn wirtualnych** > **dysków**i zaczekaj, aż hello **podłączone do** tooturn pole puste.</span><span class="sxs-lookup"><span data-stu-id="e48ef-151">Go too**Virtual Machines** > **Disks**, and wait for hello **Attached To** field tooturn blank.</span></span> <span data-ttu-id="e48ef-152">Oznacza to, że dysk hello pomyślnie została odłączona od hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e48ef-152">This indicates hello disk has successfully detached from hello VM.</span></span>
    6. <span data-ttu-id="e48ef-153">Wybierz **usunąć** u dołu hello **maszyn wirtualnych** > **dysków** toodelete hello dysku.</span><span class="sxs-lookup"><span data-stu-id="e48ef-153">Select **Delete** at hello bottom of **Virtual Machines** > **Disks** toodelete hello disk.</span></span>

  - <span data-ttu-id="e48ef-154">Jeśli hello dysk jest dyskiem systemu operacyjnego (hello **zawiera system operacyjny** pole ma wartość, takich jak system Windows) i dołączone tooa maszyny Wirtualnej, wykonaj następujące kroki hello toodelete maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e48ef-154">If hello disk is an OS disk (hello **Contains OS** field has a value like Windows) and attached tooa VM, follow these steps toodelete hello VM.</span></span> <span data-ttu-id="e48ef-155">Nie można odłączyć dysku systemu operacyjnego Hello, dzięki czemu będziemy mogli toodelete hello wirtualna toorelease hello dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="e48ef-155">hello OS disk cannot be detached, so we have toodelete hello VM toorelease hello lease.</span></span>

    1. <span data-ttu-id="e48ef-156">Sprawdź nazwę hello powitalne maszyny wirtualnej hello dysk danych jest dołączony do.</span><span class="sxs-lookup"><span data-stu-id="e48ef-156">Check hello name of hello Virtual Machine hello Data Disk is attached to.</span></span>  
    2. <span data-ttu-id="e48ef-157">Przejdź za**maszyn wirtualnych** > **wystąpień**, a następnie wybierz hello maszynę Wirtualną, która hello dysku jest dołączony do.</span><span class="sxs-lookup"><span data-stu-id="e48ef-157">Go too**Virtual Machines** > **Instances**, and then select hello VM that hello disk is attached to.</span></span>
    3. <span data-ttu-id="e48ef-158">Upewnij się, że nic nie jest aktywnie używających hello maszyny wirtualnej i czy użytkownik nie jest już konieczne hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e48ef-158">Make sure that nothing is actively using hello virtual machine, and that you no longer need hello virtual machine.</span></span>
    4. <span data-ttu-id="e48ef-159">Wybierz hello wirtualna hello dysk jest dołączony do, następnie wybierz **usunąć** > **Delete hello dołączone dyski**.</span><span class="sxs-lookup"><span data-stu-id="e48ef-159">Select hello VM hello disk is attached to, then select **Delete** > **Delete hello attached disks**.</span></span>
    5. <span data-ttu-id="e48ef-160">Przejdź za**maszyn wirtualnych** > **dysków**i zaczekaj, aż hello toodisappear dysku.</span><span class="sxs-lookup"><span data-stu-id="e48ef-160">Go too**Virtual Machines** > **Disks**, and wait for hello disk toodisappear.</span></span>  <span data-ttu-id="e48ef-161">Może potrwać kilka minut, aż ten toooccur i może być konieczne toorefresh hello strony.</span><span class="sxs-lookup"><span data-stu-id="e48ef-161">It may take a few minutes for this toooccur, and you may need toorefresh hello page.</span></span>
    6. <span data-ttu-id="e48ef-162">Jeśli dysk hello nie zniknie, poczekaj, aż hello **podłączone do** tooturn pole puste.</span><span class="sxs-lookup"><span data-stu-id="e48ef-162">If hello disk does not disappear, wait for hello **Attached To** field tooturn blank.</span></span> <span data-ttu-id="e48ef-163">Oznacza to, że dysk hello pełni została odłączona od hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e48ef-163">This indicates hello disk has fully detached from hello VM.</span></span>  <span data-ttu-id="e48ef-164">Następnie wybierz dysk hello i wybierz **usunąć** u dołu hello hello strony toodelete hello dysku.</span><span class="sxs-lookup"><span data-stu-id="e48ef-164">Then, select hello disk, and select **Delete** at hello bottom of hello page toodelete hello disk.</span></span>


   > [!NOTE]
   > <span data-ttu-id="e48ef-165">Jeśli dysk jest tooa dołączona maszyna wirtualna, nie będzie możliwe toodelete go.</span><span class="sxs-lookup"><span data-stu-id="e48ef-165">If a disk is attached tooa VM, you will not be able toodelete it.</span></span> <span data-ttu-id="e48ef-166">Dyski są odłączone asynchronicznie z usuniętych maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e48ef-166">Disks are detached from a deleted VM asynchronously.</span></span> <span data-ttu-id="e48ef-167">Może upłynąć kilka minut, po usunięciu hello maszyny Wirtualnej dla tego tooclear pole w górę.</span><span class="sxs-lookup"><span data-stu-id="e48ef-167">It might take a few minutes after hello VM is deleted for this field tooclear up.</span></span>
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-hello-storage-account-or-container"></a><span data-ttu-id="e48ef-168">Krok 2: Usuń wszelkie obrazów maszyn wirtualnych, które uniemożliwiają usunięcie konta magazynu hello lub kontenera</span><span class="sxs-lookup"><span data-stu-id="e48ef-168">Step 2: Delete any VM Images that are preventing deletion of hello storage account or container</span></span>
1. <span data-ttu-id="e48ef-169">Przełącz toohello [klasycznego portalu Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="e48ef-169">Switch toohello [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="e48ef-170">Wybierz **maszyny WIRTUALNEJ** > **obrazów**, a następnie usuń hello obrazów, które są skojarzone z kontem magazynu hello, kontenera lub wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="e48ef-170">Select **VIRTUAL MACHINE** > **IMAGES**, and then delete hello images that are associated with hello storage account, container, or VHD.</span></span>

    <span data-ttu-id="e48ef-171">Po tym spróbuj ponownie konto magazynu hello toodelete, kontenera lub wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="e48ef-171">After that, try toodelete hello storage account, container, or VHD again.</span></span>

> [!WARNING]
> <span data-ttu-id="e48ef-172">Należy się tooback zapasową wszystkich danych, które mają toosave przed usunięciem konta hello.</span><span class="sxs-lookup"><span data-stu-id="e48ef-172">Be sure tooback up anything you want toosave before you delete hello account.</span></span> <span data-ttu-id="e48ef-173">Po usunięciu wirtualnego dysku twardego, obiektów blob, tabeli, kolejki lub pliku spowoduje jego trwałe skasowanie.</span><span class="sxs-lookup"><span data-stu-id="e48ef-173">Once you delete a VHD, blob, table, queue, or file, it is permanently deleted.</span></span> <span data-ttu-id="e48ef-174">Upewnij się, że hello zasób nie jest w użyciu.</span><span class="sxs-lookup"><span data-stu-id="e48ef-174">Ensure that hello resource is not in use.</span></span>
>
>

## <a name="about-hello-stopped-deallocated-status"></a><span data-ttu-id="e48ef-175">O hello stan zatrzymane (cofnięciu przydziału)</span><span class="sxs-lookup"><span data-stu-id="e48ef-175">About hello Stopped (deallocated) status</span></span>
<span data-ttu-id="e48ef-176">Maszyny wirtualne, które zostały utworzone w hello klasycznego modelu wdrażania i zostać zatrzymane będą miały hello **zatrzymane (cofnięciu przydziału)** stan albo hello [portalu Azure](https://portal.azure.com/) lub [klasycznego portalu Azure ](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="e48ef-176">VMs that were created in hello classic deployment model and that have been retained will have hello **Stopped (deallocated)** status on either hello [Azure portal](https://portal.azure.com/) or [Azure classic portal](https://manage.windowsazure.com/).</span></span>

<span data-ttu-id="e48ef-177">**Klasyczny portal Azure**:</span><span class="sxs-lookup"><span data-stu-id="e48ef-177">**Azure classic portal**:</span></span>

![Zatrzymano stanu (Deallocated) dla maszyn wirtualnych z portalu Azure.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

<span data-ttu-id="e48ef-179">**Azure portal**:</span><span class="sxs-lookup"><span data-stu-id="e48ef-179">**Azure portal**:</span></span>

![Zatrzymana (cofnięciu przydziału) stanu dla maszyn wirtualnych w klasycznym portalu Azure.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

<span data-ttu-id="e48ef-181">Stan "Zatrzymane (cofnięciu przydziału)" zwalnia zasoby komputera hello, takie jak hello procesora CPU, pamięci i sieci.</span><span class="sxs-lookup"><span data-stu-id="e48ef-181">A "Stopped (deallocated)" status releases hello computer resources, such as hello CPU, memory, and network.</span></span> <span data-ttu-id="e48ef-182">dyski Hello, jednak są nadal przechowywane, dzięki czemu będzie można szybko utworzyć ponownie hello maszyny Wirtualnej w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="e48ef-182">hello disks, however, are still retained so that you can quickly re-create hello VM if necessary.</span></span> <span data-ttu-id="e48ef-183">Te dyski są tworzone na wirtualne dyski twarde, które bazują na magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="e48ef-183">These disks are created on top of VHDs, which are backed by Azure storage.</span></span> <span data-ttu-id="e48ef-184">Konto magazynu Hello ma te wirtualne dyski twarde i dyski hello jest dzierżawy na tych dyskach VHD.</span><span class="sxs-lookup"><span data-stu-id="e48ef-184">hello storage account has these VHDs, and hello disks have leases on those VHDs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e48ef-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e48ef-185">Next steps</span></span>
* [<span data-ttu-id="e48ef-186">Usunięcie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="e48ef-186">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
