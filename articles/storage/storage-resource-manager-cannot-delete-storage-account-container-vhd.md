---
title: "Rozwiązywanie problemów podczas usuwania konta magazynu platformy Azure, w pojemnikach lub wirtualne dyski twarde | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów podczas usuwania konta magazynu platformy Azure, w pojemnikach lub wirtualne dyski twarde"
services: storage
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: storage
ms.assetid: 17403aa1-fe8d-45ec-bc33-2c0b61126286
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 318d7146ea53a806baf813ff7de2fe91f18becc8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a><span data-ttu-id="5ff1a-103">Rozwiązywanie problemów podczas usuwania konta magazynu platformy Azure, w pojemnikach lub wirtualne dyski twarde</span><span class="sxs-lookup"><span data-stu-id="5ff1a-103">Troubleshoot errors when you delete Azure storage accounts, containers, or VHDs</span></span>

<span data-ttu-id="5ff1a-104">Może pojawić się błędy podczas próby usunięcia konta magazynu platformy Azure, kontenera lub wirtualnego dysku twardego (VHD) w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5ff1a-104">You might receive errors when you try to delete an Azure storage account, container, or virtual hard disk (VHD) in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="5ff1a-105">Ten artykuł zawiera wskazówki dotyczące rozwiązywania problemów w celu rozwiązania problemu z wdrożenia usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-105">This article provides troubleshooting guidance to help resolve the problem in an Azure Resource Manager deployment.</span></span>

<span data-ttu-id="5ff1a-106">Jeśli w tym artykule nie rozwiązania Azure problemu, odwiedź fora Azure na [MSDN i przepełnienie stosu](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="5ff1a-106">If this article doesn't address your Azure problem, visit the Azure forums on [MSDN and Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="5ff1a-107">Możesz zamieścić problemu na tych fora lub do @AzureSupport w serwisie Twitter.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-107">You can post your problem on these forums or to @AzureSupport on Twitter.</span></span> <span data-ttu-id="5ff1a-108">Ponadto można pliku żądania pomocy technicznej platformy Azure, wybierając **uzyskać pomoc techniczną** na [pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) lokacji.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-108">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="5ff1a-109">Objawy</span><span class="sxs-lookup"><span data-stu-id="5ff1a-109">Symptoms</span></span>
### <a name="scenario-1"></a><span data-ttu-id="5ff1a-110">Scenariusz 1</span><span class="sxs-lookup"><span data-stu-id="5ff1a-110">Scenario 1</span></span>
<span data-ttu-id="5ff1a-111">Podczas próby usunięcia dysku VHD na koncie magazynu w ramach wdrożenia usługi Resource Manager, pojawi się następujący komunikat o błędzie:</span><span class="sxs-lookup"><span data-stu-id="5ff1a-111">When you try to delete a VHD in a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="5ff1a-112">**Nie można usunąć obiektu blob "vhds/BlobName.vhd". Błąd: Jest obecnie dzierżawy w obiekcie blob i identyfikator dzierżawy nie został określony w żądaniu.**</span><span class="sxs-lookup"><span data-stu-id="5ff1a-112">**Failed to delete blob 'vhds/BlobName.vhd'. Error: There is currently a lease on the blob and no lease ID was specified in the request.**</span></span>

<span data-ttu-id="5ff1a-113">Ten problem może wystąpić, ponieważ maszyna wirtualna (VM) ma dzierżawę na wirtualny dysk twardy, który próbujesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-113">This problem can occur because a virtual machine (VM) has a lease on the VHD that you are trying to delete.</span></span>

### <a name="scenario-2"></a><span data-ttu-id="5ff1a-114">Scenariusz 2</span><span class="sxs-lookup"><span data-stu-id="5ff1a-114">Scenario 2</span></span>
<span data-ttu-id="5ff1a-115">Podczas próby usunięcia kontenera na koncie magazynu w ramach wdrożenia usługi Resource Manager, pojawi się następujący komunikat o błędzie:</span><span class="sxs-lookup"><span data-stu-id="5ff1a-115">When you try to delete a container in a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="5ff1a-116">**Nie można usunąć kontenera magazynu "VHD". Błąd: Jest obecnie dzierżawy w kontenerze i identyfikator dzierżawy nie został określony w żądaniu.**</span><span class="sxs-lookup"><span data-stu-id="5ff1a-116">**Failed to delete storage container 'vhds'. Error: There is currently a lease on the container and no lease ID was specified in the request.**</span></span>

<span data-ttu-id="5ff1a-117">Ten problem może wystąpić, ponieważ kontener wirtualnego dysku twardego, który jest zablokowany w stanie dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-117">This problem can occur because the container has a VHD that is locked in the lease state.</span></span>

### <a name="scenario-3"></a><span data-ttu-id="5ff1a-118">Scenariusz 3</span><span class="sxs-lookup"><span data-stu-id="5ff1a-118">Scenario 3</span></span>
<span data-ttu-id="5ff1a-119">Podczas usuwania konta magazynu w ramach wdrożenia usługi Resource Manager, pojawi się następujący komunikat o błędzie:</span><span class="sxs-lookup"><span data-stu-id="5ff1a-119">When you try to delete a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="5ff1a-120">**Nie można usunąć konta magazynu "StorageAccountName". Błąd: Nie można usunąć konta magazynu z powodu jego artefakty są nadal używane.**</span><span class="sxs-lookup"><span data-stu-id="5ff1a-120">**Failed to delete storage account 'StorageAccountName'. Error: The storage account cannot be deleted due to its artifacts being in use.**</span></span>

<span data-ttu-id="5ff1a-121">Ten problem może wystąpić, ponieważ konto magazynu zawiera wirtualny dysk twardy jest w stanie dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-121">This problem can occur because the storage account contains a VHD that is in the lease state.</span></span>

## <a name="solution"></a><span data-ttu-id="5ff1a-122">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="5ff1a-122">Solution</span></span> 
<span data-ttu-id="5ff1a-123">Aby rozwiązać te problemy, należy określić wirtualnego dysku twardego, który jest przyczyną błędu i skojarzonego VM.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-123">To resolve these problems, you must identify the VHD that is causing the error and the associated VM.</span></span> <span data-ttu-id="5ff1a-124">Następnie odłącz wirtualny dysk twardy z maszyny Wirtualnej (w przypadku dysków z danymi) lub Usuń maszynę Wirtualną, która korzysta z wirtualnego dysku twardego (dysków systemu operacyjnego).</span><span class="sxs-lookup"><span data-stu-id="5ff1a-124">Then, detach the VHD from the VM (for data disks) or delete the VM that is using the VHD (for OS disks).</span></span> <span data-ttu-id="5ff1a-125">To spowoduje usunięcie dzierżawy z wirtualnego dysku twardego i umożliwia jego do usunięcia.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-125">This removes the lease from the VHD and allows it to be deleted.</span></span> 

<span data-ttu-id="5ff1a-126">Aby to zrobić, użyj jednej z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="5ff1a-126">To do this, use one of the following methods:</span></span>

### <a name="method-1---use-azure-storage-explorer"></a><span data-ttu-id="5ff1a-127">Metoda 1 - użyj Eksploratora magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="5ff1a-127">Method 1 - Use Azure storage explorer</span></span>

### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a><span data-ttu-id="5ff1a-128">Krok 1 zidentyfikować wirtualnego dysku twardego, który uniemożliwia usunięcie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="5ff1a-128">Step 1 Identify the VHD that prevent deletion of the storage account</span></span>

1. <span data-ttu-id="5ff1a-129">Podczas usuwania konta magazynu, zostanie wyświetlony komunikat okno dialogowe podobne do poniższych:</span><span class="sxs-lookup"><span data-stu-id="5ff1a-129">When you delete the storage account, you will receive a message dialog such as the following:</span></span> 

    ![komunikat podczas usuwania konta magazynu](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="5ff1a-131">Sprawdź **adres URL dysku** do identyfikowania magazynu konto i wirtualnego dysku twardego, który uniemożliwia usunięcie konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-131">Check the **Disk URL** to identify the storage account and the VHD that prevents you delete the storage account.</span></span> <span data-ttu-id="5ff1a-132">W poniższym przykładzie ciąg przed ". blob.core.windows.net" jest nazwa konta magazynu, a Nazwa wirtualnego dysku twardego jest "SCCM2012-2015-08-28.vhd".</span><span class="sxs-lookup"><span data-stu-id="5ff1a-132">In the following example, the string before “.blob.core.windows.net “ is the storage account name, and "SCCM2012-2015-08-28.vhd" is the VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-the-vhd-by-using-azure-storage-explorer"></a><span data-ttu-id="5ff1a-133">Krok 2 usunąć wirtualny dysk twardy za pomocą Eksploratora usługi Storage platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5ff1a-133">Step 2 Delete the VHD by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="5ff1a-134">Pobierz i zainstaluj najnowszą wersję [Eksploratora usługi Storage Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="5ff1a-134">Download and Install the latest version of [Azure Storage Explorer](http://storageexplorer.com/).</span></span> <span data-ttu-id="5ff1a-135">To narzędzie jest aplikacją autonomiczną firmy Microsoft, która pozwala łatwo pracować z danymi usługi Azure Storage w systemie Windows, system macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-135">This tool is a standalone app from Microsoft that allows you to easily work with Azure Storage data on Windows, macOS and Linux.</span></span>
2. <span data-ttu-id="5ff1a-136">Otwórz Eksploratora usługi Storage platformy Azure, wybierz opcję</span><span class="sxs-lookup"><span data-stu-id="5ff1a-136">Open Azure Storage Explorer, select</span></span> ![Ikona konta](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) <span data-ttu-id="5ff1a-138">na pasku po lewej stronie wybierz środowisku platformy Azure, a następnie zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-138">on the left bar, select your Azure environment, and then sign in.</span></span>

3. <span data-ttu-id="5ff1a-139">Wybierz wszystkie subskrypcje lub subskrypcji, która zawiera konta magazynu, który chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-139">Select all subscriptions or the subscription that contains the storage account you want to delete.</span></span>

    ![Dodaj subskrypcję](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. <span data-ttu-id="5ff1a-141">Przejdź do uzyskiwanej w adresie URL dysku wcześniej, wybierz konto magazynu **kontenerów obiektów Blob** > **wirtualne dyski twarde** i wyszukaj wirtualnego dysku twardego, który uniemożliwia usunięcie konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-141">Go to the storage account that we obtained from the disk URL earlier, select the **Blob Containers** > **vhds** and search for the VHD that prevents you delete the storage account.</span></span>
5. <span data-ttu-id="5ff1a-142">Jeśli zostanie znaleziony wirtualny dysk twardy, sprawdź **nazwę maszyny Wirtualnej** kolumny można znaleźć maszyny Wirtualnej, który używa tego wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-142">If the VHD is found,  check the **VM Name** column to find the VM that is using this VHD.</span></span>

    ![Sprawdź maszyny wirtualnej](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. <span data-ttu-id="5ff1a-144">Usuń dzierżawy z dysku VHD za pomocą portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-144">Remove the lease from the VHD by using Azure portal.</span></span> <span data-ttu-id="5ff1a-145">Aby uzyskać więcej informacji, zobacz [Usuń dzierżawy z wirtualnego dysku twardego](#remove-the-lease-from-the-vhd).</span><span class="sxs-lookup"><span data-stu-id="5ff1a-145">For more information, see [Remove the lease from the VHD](#remove-the-lease-from-the-vhd).</span></span> 

7. <span data-ttu-id="5ff1a-146">Przejdź do Eksploratora magazynu Azure, kliknij prawym przyciskiem myszy dysk VHD, a następnie wybierz delete.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-146">Go to the Azure Storage Explorer, right-click the VHD and then select delete.</span></span>

8. <span data-ttu-id="5ff1a-147">Usuwa konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-147">Delete the storage account.</span></span>

### <a name="method-2---use-azure-portal"></a><span data-ttu-id="5ff1a-148">Metoda 2 - użyj portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5ff1a-148">Method 2 - Use Azure portal</span></span> 

#### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a><span data-ttu-id="5ff1a-149">: Krok 1 wirtualny dysk twardy, który uniemożliwia usunięcie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="5ff1a-149">Step 1: Identify the VHD that prevent deletion of the storage account</span></span>

1. <span data-ttu-id="5ff1a-150">Podczas usuwania konta magazynu, zostanie wyświetlony komunikat okno dialogowe podobne do poniższych:</span><span class="sxs-lookup"><span data-stu-id="5ff1a-150">When you delete the storage account, you will receive a message dialog such as the following:</span></span> 

    ![komunikat podczas usuwania konta magazynu](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="5ff1a-152">Sprawdź **adres URL dysku** do identyfikowania magazynu konto i wirtualnego dysku twardego, który uniemożliwia usunięcie konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-152">Check the **Disk URL** to identify the storage account and the VHD that prevents you delete the storage account.</span></span> <span data-ttu-id="5ff1a-153">W poniższym przykładzie ciąg przed ". blob.core.windows.net" jest nazwa konta magazynu, a Nazwa wirtualnego dysku twardego jest "SCCM2012-2015-08-28.vhd".</span><span class="sxs-lookup"><span data-stu-id="5ff1a-153">In the following example, the string before “.blob.core.windows.net “ is the storage account name, and "SCCM2012-2015-08-28.vhd" is the VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. <span data-ttu-id="5ff1a-154">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5ff1a-154">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
3. <span data-ttu-id="5ff1a-155">W menu Centrum wybierz **wszystkie zasoby**.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-155">On the Hub menu, select **All resources**.</span></span> <span data-ttu-id="5ff1a-156">Przejdź do konta magazynu, a następnie wybierz **obiekty BLOB** > **wirtualne dyski twarde**.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-156">Go to the storage account, and then select **Blobs** > **vhds**.</span></span>

    ![Zrzut ekranu przedstawiający portal, konto magazynu i kontener "VHD" wyróżnione](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. <span data-ttu-id="5ff1a-158">Odszukaj wirtualny dysk twardy, który mamy uzyskany z adresu URL dysku wcześniej.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-158">Locate the VHD that we obtained from the disk URL earlier.</span></span> <span data-ttu-id="5ff1a-159">Następnie określ, którego używa wirtualna wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-159">Then, determine which VM is using the VHD.</span></span> <span data-ttu-id="5ff1a-160">Zazwyczaj można określić, której maszyna wirtualna znajduje się wirtualny dysk twardy sprawdzana jest nazwa wirtualnego dysku twardego:</span><span class="sxs-lookup"><span data-stu-id="5ff1a-160">Usually, you can determine which VM holds the VHD by checking name of the VHD:</span></span>

<span data-ttu-id="5ff1a-161">Maszyna wirtualna w modelu programowania usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5ff1a-161">VM in Resource Manager development  model</span></span>

   * <span data-ttu-id="5ff1a-162">Dysków systemu operacyjnego należy wykonać tę konwencję nazewnictwa: VMName-RRRR-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="5ff1a-162">OS disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="5ff1a-163">Dyski danych należy wykonać tę konwencję nazewnictwa: VMName-RRRR-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="5ff1a-163">Data disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

<span data-ttu-id="5ff1a-164">Maszynę Wirtualną w klasycznym modelu programowania</span><span class="sxs-lookup"><span data-stu-id="5ff1a-164">VM in Classic development model</span></span>

   * <span data-ttu-id="5ff1a-165">Dysków systemu operacyjnego należy wykonać tę konwencję nazewnictwa: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="5ff1a-165">OS disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="5ff1a-166">Dyski danych należy wykonać tę konwencję nazewnictwa: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="5ff1a-166">Data disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

#### <a name="step-2-remove-the-lease-from-the-vhd"></a><span data-ttu-id="5ff1a-167">Krok 2: Usuń dzierżawy z wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="5ff1a-167">Step 2: Remove the lease from the VHD</span></span>

<span data-ttu-id="5ff1a-168">[Usuń dzierżawy z wirtualnego dysku twardego](#remove-the-lease-from-the-vhd), a następnie usunąć konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-168">[Remove the lease from the VHD](#remove-the-lease-from-the-vhd), and then delete the storage account.</span></span>

## <a name="what-is-a-lease"></a><span data-ttu-id="5ff1a-169">Co to jest dzierżawa?</span><span class="sxs-lookup"><span data-stu-id="5ff1a-169">What is a lease?</span></span>
<span data-ttu-id="5ff1a-170">Dzierżawa jest blokady, który może służyć do kontrolowania dostępu do obiektów blob (na przykład dysk VHD).</span><span class="sxs-lookup"><span data-stu-id="5ff1a-170">A lease is a lock that can be used to control access to a blob (for example, a VHD).</span></span> <span data-ttu-id="5ff1a-171">Gdy obiektu blob jest dzierżawiony, właściciele dzierżawy może uzyskać dostęp do obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-171">When a blob is leased, only the owners of the lease can access the blob.</span></span> <span data-ttu-id="5ff1a-172">Dzierżawa jest ważne z następujących powodów:</span><span class="sxs-lookup"><span data-stu-id="5ff1a-172">A lease is important for the following reasons:</span></span>

* <span data-ttu-id="5ff1a-173">Zapobiega uszkodzenie danych, jeśli wiele właścicieli spróbuj zapisać tę samą część obiektu blob w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-173">It prevents data corruption if multiple owners try to write to the same portion of the blob at the same time.</span></span>
* <span data-ttu-id="5ff1a-174">Obiekt blob uniemożliwia usuwany, jeśli coś aktywnie używa go (na przykład maszyn wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="5ff1a-174">It prevents the blob from being deleted if something is actively using it (for example, a VM).</span></span>
* <span data-ttu-id="5ff1a-175">Konto magazynu uniemożliwia usuwany, jeśli coś aktywnie używa go (na przykład maszyn wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="5ff1a-175">It prevents the storage account from being deleted if something is actively using it (for example, a VM).</span></span>

### <a name="remove-the-lease-from-the-vhd"></a><span data-ttu-id="5ff1a-176">Usuń dzierżawy z wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="5ff1a-176">Remove the lease from the VHD</span></span>
<span data-ttu-id="5ff1a-177">Jeśli wirtualny dysk twardy, dysk systemu operacyjnego, należy usunąć maszynę Wirtualną, aby usunąć dzierżawy:</span><span class="sxs-lookup"><span data-stu-id="5ff1a-177">If the VHD is an OS disk, you must delete the VM to remove the lease:</span></span>

1. <span data-ttu-id="5ff1a-178">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5ff1a-178">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5ff1a-179">Na **Centrum** menu, wybierz opcję **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-179">On the **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="5ff1a-180">Wybierz maszynę Wirtualną, która przechowuje dzierżawę na dysku VHD.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-180">Select the VM that holds a lease on the VHD.</span></span>
4. <span data-ttu-id="5ff1a-181">Upewnij się, że nic nie jest aktywnie przy użyciu maszyny wirtualnej i nie są już potrzebne maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-181">Make sure that nothing is actively using the virtual machine, and that you no longer need the virtual machine.</span></span>
5. <span data-ttu-id="5ff1a-182">W górnej części **szczegóły maszyny Wirtualnej** bloku, wybierz opcję **usunąć**, a następnie kliknij przycisk **tak** o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-182">At the top of the **VM details** blade, select **Delete**, and then click **Yes** to confirm.</span></span>
6. <span data-ttu-id="5ff1a-183">Maszyna wirtualna powinien zostać usunięty, ale wirtualnego dysku twardego mogą być przechowywane.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-183">The VM should be deleted, but the VHD can be retained.</span></span> <span data-ttu-id="5ff1a-184">Jednak dysku VHD nie powinni mieć dzierżawę na nim.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-184">However, the VHD should no longer have a lease on it.</span></span> <span data-ttu-id="5ff1a-185">Może upłynąć kilka minut, aż dzierżawa do zwolnienia.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-185">It may take a few minutes for the lease to be released.</span></span> <span data-ttu-id="5ff1a-186">Aby zweryfikować, że zwolnieniu dzierżawy, przejdź do **wszystkie zasoby** > **nazwy konta magazynu** > **obiekty BLOB**  >   **wirtualne dyski twarde**.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-186">To verify that the lease is released, go to **All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="5ff1a-187">W **właściwości obiektu Blob** okienku **stanu dzierżawy** wartość powinna być **odblokowany**.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-187">In the **Blob properties** pane, the **Lease Status** value should be **Unlocked**.</span></span>

<span data-ttu-id="5ff1a-188">Jeśli wirtualny dysk twardy jest dysk z danymi, odłącz wirtualny dysk twardy z maszyny Wirtualnej, aby usunąć dzierżawy:</span><span class="sxs-lookup"><span data-stu-id="5ff1a-188">If the VHD is a data disk, detach the VHD from the VM to remove the lease:</span></span>

1. <span data-ttu-id="5ff1a-189">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5ff1a-189">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5ff1a-190">Na **Centrum** menu, wybierz opcję **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-190">On the **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="5ff1a-191">Wybierz maszynę Wirtualną, która przechowuje dzierżawę na dysku VHD.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-191">Select the VM that holds a lease on the VHD.</span></span>
4. <span data-ttu-id="5ff1a-192">Wybierz **dysków** na **szczegóły maszyny Wirtualnej** bloku.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-192">Select **Disks** on the **VM details** blade.</span></span>
5. <span data-ttu-id="5ff1a-193">Wybierz dysk danych, który przechowuje dzierżawę na dysku VHD.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-193">Select the data disk that holds a lease on the VHD.</span></span> <span data-ttu-id="5ff1a-194">Można określić, który wirtualny dysk twardy jest podłączony w dysku, sprawdzając adres URL dysku VHD.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-194">You can determine which VHD is attached in the disk by checking the URL of the VHD.</span></span>
6. <span data-ttu-id="5ff1a-195">Określ, z pewnością, że nic nie jest aktywnie przy użyciu dysku danych.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-195">Determine with certainty that nothing is actively using the data disk.</span></span>
7. <span data-ttu-id="5ff1a-196">Kliknij przycisk **Detach** na **dysku szczegóły** bloku.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-196">Click **Detach** on the **Disk details** blade.</span></span>
8. <span data-ttu-id="5ff1a-197">Dysk powinien teraz można odłączyć od maszyny Wirtualnej, i wirtualnego dysku twardego nie może mieć dzierżawę na nim.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-197">The disk should now be detached from the VM, and the VHD should no longer have a lease on it.</span></span> <span data-ttu-id="5ff1a-198">Może upłynąć kilka minut, aż dzierżawa do zwolnienia.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-198">It may take a few minutes for the lease to be released.</span></span> <span data-ttu-id="5ff1a-199">Aby zweryfikować zwolnienie dzierżawy, przejdź do **wszystkie zasoby** > **nazwy konta magazynu** > **obiekty BLOB**  >  **wirtualne dyski twarde**.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-199">To verify that the lease has been released, go to **All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="5ff1a-200">W **właściwości obiektu Blob** okienku **stanu dzierżawy** wartość powinna być **odblokowany**.</span><span class="sxs-lookup"><span data-stu-id="5ff1a-200">In the **Blob properties** pane, the **Lease Status** value should be **Unlocked**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ff1a-201">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5ff1a-201">Next steps</span></span>
* [<span data-ttu-id="5ff1a-202">Usunięcie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="5ff1a-202">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
* [<span data-ttu-id="5ff1a-203">Sposób podziału zablokowanym dzierżawy magazynu obiektów blob na platformie Microsoft Azure (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="5ff1a-203">How to break the locked lease of blob storage in Microsoft Azure (PowerShell)</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
