---
title: "aaaUpload wirtualnego dysku twardego pliku tooAzure DevTest Labs przy użyciu narzędzia AzCopy | Dokumentacja firmy Microsoft"
description: "Przekaż toolab pliku wirtualnego dysku twardego konto magazynu przy użyciu narzędzia AzCopy"
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
ms.openlocfilehash: 14f9e933b0bd27451f6bcb94841ecc381213e578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-azcopy"></a><span data-ttu-id="8013d-103">Przekaż toolab pliku wirtualnego dysku twardego konto magazynu przy użyciu narzędzia AzCopy</span><span class="sxs-lookup"><span data-stu-id="8013d-103">Upload VHD file toolab's storage account using AzCopy</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="8013d-104">W usłudze Azure DevTest Labs pliki wirtualnego dysku twardego mogą być używane toocreate niestandardowych obrazów, które są używane tooprovision maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="8013d-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="8013d-105">Hello następujące kroki opisano przy użyciu tooupload narzędzia wiersza polecenia AzCopy hello wirtualnego dysku twardego pliku tooa laboratorium dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="8013d-105">hello following steps walk you through using hello AzCopy command-line utility tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="8013d-106">Po przesłaniu pliku wirtualnego dysku twardego hello [następne kroki sekcji](#next-steps) wymieniono niektóre artykuły, które przedstawiają sposób toocreate niestandardowego obrazu z hello przekazany plik VHD.</span><span class="sxs-lookup"><span data-stu-id="8013d-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="8013d-107">Aby uzyskać więcej informacji o dyskach i wirtualne dyski twarde na platformie Azure, zobacz [o dyskach i wirtualne dyski twarde dla maszyn wirtualnych](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="8013d-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

> [!NOTE] 
>  
> <span data-ttu-id="8013d-108">Narzędzie AzCopy to narzędzie wiersza polecenia systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="8013d-108">AzCopy is a Windows-only command-line utility.</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="8013d-109">Instrukcje krok po kroku</span><span class="sxs-lookup"><span data-stu-id="8013d-109">Step-by-step instructions</span></span>

<span data-ttu-id="8013d-110">Witaj, wykonując kroki przeszukiwania plików podczas przekazywania wirtualnego dysku twardego tooAzure DevTest Labs przy użyciu [AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="8013d-110">hello following steps walk you through uploading a VHD file tooAzure DevTest Labs using [AzCopy](http://aka.ms/downloadazcopy).</span></span> 

1. <span data-ttu-id="8013d-111">Pobierz hello nazwę konta magazynu laboratorium hello za pośrednictwem hello portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="8013d-111">Get hello name of hello lab's storage account using hello Azure portal:</span></span>

1. <span data-ttu-id="8013d-112">Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="8013d-112">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="8013d-113">Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.</span><span class="sxs-lookup"><span data-stu-id="8013d-113">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="8013d-114">Z listy hello labs wybierz żądany laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="8013d-114">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="8013d-115">W bloku hello laboratorium, wybierz **konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="8013d-115">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="8013d-116">W laboratorium hello **konfiguracji** bloku, wybierz opcję **niestandardowych obrazów (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="8013d-116">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="8013d-117">Na powitania **niestandardowych obrazów** bloku, wybierz **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="8013d-117">On hello **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="8013d-118">Na powitania **obraz niestandardowy** bloku, wybierz opcję **wirtualnego dysku twardego**.</span><span class="sxs-lookup"><span data-stu-id="8013d-118">On hello **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="8013d-119">Na powitania **wirtualnego dysku twardego** bloku, wybierz opcję **przekazania dysku VHD za pomocą programu PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="8013d-119">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Przekaż plik VHD za pomocą programu PowerShell](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. <span data-ttu-id="8013d-121">Witaj **przekazywanie obrazu za pomocą programu PowerShell** bloku Wyświetla toohello wywołania **Add-AzureVhd** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8013d-121">hello **Upload an image using PowerShell** blade displays a call toohello **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="8013d-122">Witaj pierwszy parametr (*docelowego*) zawiera hello identyfikatora URI dla kontenera obiektów blob (*przekazuje*) w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="8013d-122">hello first parameter (*Destination*) contains hello URI for a blob container (*uploads*) in hello following format:</span></span>

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. <span data-ttu-id="8013d-123">Zwróć uwagę na powitania pełny identyfikator URI, ponieważ jest używana w dalszych krokach.</span><span class="sxs-lookup"><span data-stu-id="8013d-123">Make note of hello full URI as it is used in later steps.</span></span>

1. <span data-ttu-id="8013d-124">Przekaż plik VHD hello przy użyciu narzędzia AzCopy:</span><span class="sxs-lookup"><span data-stu-id="8013d-124">Upload hello VHD file using AzCopy:</span></span>
 
1. <span data-ttu-id="8013d-125">[Pobierz i zainstaluj najnowszą wersję programu AzCopy, hello](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="8013d-125">[Download and install hello latest version of AzCopy](http://aka.ms/downloadazcopy).</span></span>

1. <span data-ttu-id="8013d-126">Otwórz okno polecenia i przejdź do katalogu instalacyjnego toohello AzCopy.</span><span class="sxs-lookup"><span data-stu-id="8013d-126">Open a command window and navigate toohello AzCopy installation directory.</span></span> <span data-ttu-id="8013d-127">Opcjonalnie można dodać ścieżki systemu tooyour lokalizacji instalacji hello AzCopy.</span><span class="sxs-lookup"><span data-stu-id="8013d-127">Optionally, you can add hello AzCopy installation location tooyour system path.</span></span> <span data-ttu-id="8013d-128">Narzędzie AzCopy jest domyślnie zainstalowany toohello następującego katalogu:</span><span class="sxs-lookup"><span data-stu-id="8013d-128">By default, AzCopy is installed toohello following directory:</span></span>

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. <span data-ttu-id="8013d-129">Przy użyciu hello konta obiektów blob i kluczy kontenera magazynu identyfikatora URI, uruchom następujące polecenie w wierszu polecenia hello hello.</span><span class="sxs-lookup"><span data-stu-id="8013d-129">Using hello storage account key and blob container URI, run hello following command at hello command prompt.</span></span> <span data-ttu-id="8013d-130">Witaj *vhdFileName* . wartość musi toobe w cudzysłowy.</span><span class="sxs-lookup"><span data-stu-id="8013d-130">hello *vhdFileName* value needs toobe in quotes.</span></span> <span data-ttu-id="8013d-131">proces Hello przekazywania pliku wirtualnego dysku twardego może być długi w zależności od rozmiaru hello hello pliku wirtualnego dysku twardego i szybkość połączenia.</span><span class="sxs-lookup"><span data-stu-id="8013d-131">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span>   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a><span data-ttu-id="8013d-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8013d-132">Next steps</span></span>

- [<span data-ttu-id="8013d-133">Utworzyć obraz niestandardowy w usłudze Azure DevTest Labs z pliku VHD za pomocą hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8013d-133">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="8013d-134">Utworzyć obraz niestandardowy w usłudze Azure DevTest Labs z pliku VHD za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="8013d-134">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)