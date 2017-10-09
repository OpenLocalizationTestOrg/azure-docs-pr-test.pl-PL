---
title: "aaaUpload wirtualnego dysku twardego pliku tooAzure DevTest Labs za pomocą Eksploratora usługi Microsoft Azure Storage | Dokumentacja firmy Microsoft"
description: "Przekaż toolab pliku wirtualnego dysku twardego konto magazynu przy użyciu Eksploratora magazynu Microsoft Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 686691e3676cea4b2d7cd8bf045bc43a792c667e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-microsoft-azure-storage-explorer"></a><span data-ttu-id="082cc-103">Przekaż toolab pliku wirtualnego dysku twardego konto magazynu przy użyciu Eksploratora magazynu Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="082cc-103">Upload VHD file toolab's storage account using Microsoft Azure Storage Explorer</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="082cc-104">W usłudze Azure DevTest Labs pliki wirtualnego dysku twardego mogą być używane toocreate niestandardowych obrazów, które są używane tooprovision maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="082cc-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="082cc-105">W tym artykule przedstawiono sposób toouse [Eksploratora usługi Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md) konta magazynu laboratorium tooa pliku tooupload dysku VHD.</span><span class="sxs-lookup"><span data-stu-id="082cc-105">This article illustrates how toouse [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="082cc-106">Po przesłaniu pliku wirtualnego dysku twardego hello [następne kroki sekcji](#next-steps) wymieniono niektóre artykuły, które przedstawiają sposób toocreate niestandardowego obrazu z hello przekazany plik VHD.</span><span class="sxs-lookup"><span data-stu-id="082cc-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="082cc-107">Aby uzyskać więcej informacji o dyskach i wirtualne dyski twarde na platformie Azure, zobacz [o dyskach i wirtualne dyski twarde dla maszyn wirtualnych](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="082cc-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="082cc-108">Instrukcje krok po kroku</span><span class="sxs-lookup"><span data-stu-id="082cc-108">Step-by-step instructions</span></span>

<span data-ttu-id="082cc-109">Witaj, wykonując kroki przeszukiwania plików podczas przekazywania wirtualnego dysku twardego Labs tooDevTest przy użyciu [Eksploratora usługi Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="082cc-109">hello following steps walk you through uploading a VHD file tooDevTest Labs using [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>

1. <span data-ttu-id="082cc-110">[Pobierz i zainstaluj najnowszą wersję hello Eksploratora usługi Microsoft Azure Storage hello](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="082cc-110">[Download and install hello latest version of hello Microsoft Azure Storage Explorer](http://www.storageexplorer.com).</span></span>

1. <span data-ttu-id="082cc-111">Pobierz hello nazwę konta magazynu laboratorium hello za pośrednictwem hello portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="082cc-111">Get hello name of hello lab's storage account using hello Azure portal:</span></span>

    1. <span data-ttu-id="082cc-112">Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="082cc-112">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
    
    1. <span data-ttu-id="082cc-113">Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.</span><span class="sxs-lookup"><span data-stu-id="082cc-113">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>
    
    1. <span data-ttu-id="082cc-114">Z listy hello labs wybierz żądany laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="082cc-114">From hello list of labs, select hello desired lab.</span></span>  
    
    1. <span data-ttu-id="082cc-115">W bloku hello laboratorium, wybierz **konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="082cc-115">On hello lab's blade, select **Configuration**.</span></span> 
    
    1. <span data-ttu-id="082cc-116">W laboratorium hello **konfiguracji** bloku, wybierz opcję **niestandardowych obrazów (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="082cc-116">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>
    
    1. <span data-ttu-id="082cc-117">Na powitania **niestandardowych obrazów** bloku, wybierz **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="082cc-117">On hello **Custom images** blade, Select **+Add**.</span></span> 
    
    1. <span data-ttu-id="082cc-118">Na powitania **obraz niestandardowy** bloku, wybierz opcję **wirtualnego dysku twardego**.</span><span class="sxs-lookup"><span data-stu-id="082cc-118">On hello **Custom image** blade, select **VHD**.</span></span>
    
    1. <span data-ttu-id="082cc-119">Na powitania **wirtualnego dysku twardego** bloku, wybierz opcję **przekazania dysku VHD za pomocą programu PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="082cc-119">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>
    
        ![Przekaż plik VHD za pomocą programu PowerShell][0]
    
    1. <span data-ttu-id="082cc-121">Witaj **przekazywanie obrazu za pomocą programu PowerShell** bloku Wyświetla toohello wywołania **Add-AzureVhd** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="082cc-121">hello **Upload an image using PowerShell** blade displays a call toohello **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="082cc-122">Witaj pierwszy parametr (*docelowego*) zawiera nazwę konta magazynu hello laboratorium hello w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="082cc-122">hello first parameter (*Destination*) contains hello storage account name for hello lab in hello following format:</span></span>
    
        <span data-ttu-id="082cc-123">https://<Storage-ACCOUNT-name>.blob.Core.Windows.NET/Uploads/...</span><span class="sxs-lookup"><span data-stu-id="082cc-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span></span> 

    1. <span data-ttu-id="082cc-124">Zwróć uwagę na nazwy konta magazynu hello, ponieważ jest używana w dalszych krokach.</span><span class="sxs-lookup"><span data-stu-id="082cc-124">Make note of hello storage account name as it is used in later steps.</span></span>
    
1. <span data-ttu-id="082cc-125">Połącz tooan konta subskrypcji platformy Azure przy użyciu Eksploratora usługi Storage.</span><span class="sxs-lookup"><span data-stu-id="082cc-125">Connect tooan Azure subscription account using Storage Explorer.</span></span>

    > [!TIP] 
    > 
    > <span data-ttu-id="082cc-126">Eksplorator usługi Storage obsługuje kilka opcji połączeń.</span><span class="sxs-lookup"><span data-stu-id="082cc-126">Storage Explorer supports several connection options.</span></span> <span data-ttu-id="082cc-127">W tej części przedstawiono łączącego tooa konta magazynu skojarzone z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="082cc-127">This section illustrates connecting tooa storage account associated with your Azure subscription.</span></span> <span data-ttu-id="082cc-128">toosee hello inne opcje połączenia obsługiwane przez Eksploratora usługi Storage, zobacz artykuł toohello [wprowadzenie do Eksploratora usługi Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="082cc-128">toosee hello other connection options supported by Storage Explorer, refer toohello article, [Getting started with Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>
 
    1. <span data-ttu-id="082cc-129">Otwórz Eksploratora usługi Storage.</span><span class="sxs-lookup"><span data-stu-id="082cc-129">Open Storage Explorer.</span></span>
    
    1. <span data-ttu-id="082cc-130">W Eksploratorze usługi Storage, wybierz **ustawienia konta Azure**.</span><span class="sxs-lookup"><span data-stu-id="082cc-130">In Storage Explorer, select **Azure Account settings**.</span></span> 
    
        ![Ustawienia konta platformy Azure][1]
    
    1. <span data-ttu-id="082cc-132">w okienku po lewej stronie powitania Wyświetla kont Microsoft hello, do których logujesz się do.</span><span class="sxs-lookup"><span data-stu-id="082cc-132">hello left pane displays hello Microsoft accounts you've logged in to.</span></span> <span data-ttu-id="082cc-133">Konto tooanother tooconnect, wybierz opcję **Dodaj konto**i wykonaj hello toosign okien dialogowych za pomocą konta Microsoft, który jest skojarzony z co najmniej jedną aktywną subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="082cc-133">tooconnect tooanother account, select **Add an account**, and follow hello dialogs toosign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>
    
        ![Dodaj konto][2]
    
    1. <span data-ttu-id="082cc-135">Po pomyślnym zalogowaniu się przy użyciu konta Microsoft, w okienku po lewej stronie powitania wypełnia hello subskrypcji platformy Azure skojarzonych z tym kontem.</span><span class="sxs-lookup"><span data-stu-id="082cc-135">Once you successfully sign in with a Microsoft account, hello left pane populates with hello Azure subscriptions associated with that account.</span></span> <span data-ttu-id="082cc-136">Wybierz hello subskrypcji platformy Azure, z którymi mają toowork, a następnie wybierz **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="082cc-136">Select hello Azure subscriptions with which you want toowork, and then select **Apply**.</span></span> <span data-ttu-id="082cc-137">(Wybieranie **wszystkie subskrypcje** przełącza hello wybór wszystkich lub brak hello wymienionych subskrypcji platformy Azure.)</span><span class="sxs-lookup"><span data-stu-id="082cc-137">(Selecting **All subscriptions** toggles hello selection of all or none of hello listed Azure subscriptions.)</span></span>
    
        ![Wybieranie subskrypcji platformy Azure][3]
    
    1. <span data-ttu-id="082cc-139">w okienku po lewej stronie powitania Wyświetla hello konta magazynu skojarzone z hello wybrane subskrypcje platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="082cc-139">hello left pane displays hello storage accounts associated with hello selected Azure subscriptions.</span></span>
    
        ![Wybrane subskrypcje platformy Azure][4]

1. <span data-ttu-id="082cc-141">Zlokalizuj konto magazynu laboratorium hello:</span><span class="sxs-lookup"><span data-stu-id="082cc-141">Locate hello lab's storage account:</span></span>

    1. <span data-ttu-id="082cc-142">W okienku po lewej stronie Eksploratora usługi Storage hello Znajdź i rozwinąć węzeł hello hello subskrypcji platformy Azure, który jest właścicielem hello laboratorium.</span><span class="sxs-lookup"><span data-stu-id="082cc-142">In hello Storage Explorer left pane, locate, and expand hello node for hello Azure subscription that owns hello lab.</span></span>
    
    1. <span data-ttu-id="082cc-143">W węźle subskrypcji hello rozwiń **kont magazynu**.</span><span class="sxs-lookup"><span data-stu-id="082cc-143">Under hello subscription's node, expand **Storage Accounts**.</span></span>

    1. <span data-ttu-id="082cc-144">Rozwiń węzły konta magazynu laboratorium hello tooreveal węzła dla **kontenerów obiektów Blob**, **udziałów plików**, **kolejek**, i **tabel**.</span><span class="sxs-lookup"><span data-stu-id="082cc-144">Expand hello lab's storage account node tooreveal nodes for **Blob Containers**, **File Shares**, **Queues**, and **Tables**.</span></span>
    
    1. <span data-ttu-id="082cc-145">Rozwiń węzeł hello **kontenerów obiektów Blob** węzła.</span><span class="sxs-lookup"><span data-stu-id="082cc-145">Expand hello **Blob Containers** node.</span></span>
    
    1. <span data-ttu-id="082cc-146">Zaznacz zawartością toodisplay kontenera obiektów blob przekazywania hello w okienku po prawej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="082cc-146">Select hello uploads blob container toodisplay its contents in hello right pane.</span></span>
        
        ![Przekaż katalogu][5]

1. <span data-ttu-id="082cc-148">Przekaż plik VHD hello za pomocą Eksploratora usługi Storage:</span><span class="sxs-lookup"><span data-stu-id="082cc-148">Upload hello VHD file using Storage Explorer:</span></span>

    1. <span data-ttu-id="082cc-149">W prawym okienku Eksploratora usługi Storage hello powinna zostać wyświetlona listę obiektów blob hello w hello **przekazuje** kontenera obiektów blob z konta magazynu laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="082cc-149">In hello Storage Explorer right pane, you should see a listing of hello blobs in hello **uploads** blob container of hello lab's storage account.</span></span> <span data-ttu-id="082cc-150">Na powitania paska narzędzi edytora obiektów blob, wybierz **Przekaż**</span><span class="sxs-lookup"><span data-stu-id="082cc-150">On hello blob editor toolbar, select **Upload**</span></span> 
        
        ![Przekaż przycisku][6]
    
    1. <span data-ttu-id="082cc-152">Z hello **przekazać** menu rozwijanego wybierz **przekazywania plików...** .</span><span class="sxs-lookup"><span data-stu-id="082cc-152">From hello **Upload** drop-down menu, select **Upload files...**.</span></span>
    
    1. <span data-ttu-id="082cc-153">Na powitania **przekazać pliki** okno dialogowe, wybierz hello wielokropka.</span><span class="sxs-lookup"><span data-stu-id="082cc-153">On hello **Upload files** dialog, select hello ellipsis.</span></span>
        
        ![Wybierz plik][8]  

    1. <span data-ttu-id="082cc-155">Na powitania **tooupload wybierz pliki** okna dialogowego, przeglądania toohello żądanego pliku VHD, zaznacz go, a następnie wybierz **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="082cc-155">On hello **Select files tooupload** dialog, browse toohello desired VHD file, select it, and then select **Open**.</span></span>
    
    1. <span data-ttu-id="082cc-156">Gdy zwrócił toohello **przekazać pliki** okna dialogowego, zmień **typu obiektu Blob** za**stronicowych obiektów Blob**.</span><span class="sxs-lookup"><span data-stu-id="082cc-156">When returned toohello **Upload files** dialog, change **Blob type** too**Page Blob**.</span></span>
    
    1. <span data-ttu-id="082cc-157">Wybierz pozycję **Przekaż**.</span><span class="sxs-lookup"><span data-stu-id="082cc-157">Select **Upload**.</span></span>

        ![Wybierz plik][9]  
    
    1. <span data-ttu-id="082cc-159">Witaj Eksploratora usługi Storage **dziennik aktywności** w okienku zostaną wyświetlone stan pobierania hello (wraz z łącza toocancel hello przekazywania).</span><span class="sxs-lookup"><span data-stu-id="082cc-159">hello Storage Explorer **Activity Log** pane shows hello download status (along with links toocancel hello upload).</span></span> <span data-ttu-id="082cc-160">proces Hello przekazywania pliku wirtualnego dysku twardego może być długi w zależności od rozmiaru hello hello pliku wirtualnego dysku twardego i szybkość połączenia.</span><span class="sxs-lookup"><span data-stu-id="082cc-160">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span> 

        ![Stan przekazywania pliku][10]  

## <a name="next-steps"></a><span data-ttu-id="082cc-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="082cc-162">Next steps</span></span>

- [<span data-ttu-id="082cc-163">Utworzyć obraz niestandardowy w usłudze Azure DevTest Labs z pliku VHD za pomocą hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="082cc-163">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="082cc-164">Utworzyć obraz niestandardowy w usłudze Azure DevTest Labs z pliku VHD za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="082cc-164">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

[0]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-image-using-psh.png
[1]: ./media/devtest-lab-upload-vhd-using-storage-explorer/settings-icon.png
[2]: ./media/devtest-lab-upload-vhd-using-storage-explorer/add-account-link.png
[3]: ./media/devtest-lab-upload-vhd-using-storage-explorer/subscriptions-list.png
[4]: ./media/devtest-lab-upload-vhd-using-storage-explorer/storage-accounts-list.png
[5]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-dir.png
[6]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-button.png
[7]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-files.png
[8]: ./media/devtest-lab-upload-vhd-using-storage-explorer/select-file.png
[9]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-file.png
[10]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-status.png
