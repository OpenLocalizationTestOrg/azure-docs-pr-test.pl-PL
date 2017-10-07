---
title: "aaaUpload wirtualnego dysku twardego pliku tooAzure DevTest Labs przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Przekaż toolab pliku wirtualnego dysku twardego konto magazynu przy użyciu programu PowerShell"
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
ms.openlocfilehash: 9c3ee96e212457b0ef8203714b419350cb97f895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-powershell"></a><span data-ttu-id="d6cf7-103">Przekaż toolab pliku wirtualnego dysku twardego konto magazynu przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6cf7-103">Upload VHD file toolab's storage account using PowerShell</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="d6cf7-104">W usłudze Azure DevTest Labs pliki wirtualnego dysku twardego mogą być używane toocreate niestandardowych obrazów, które są używane tooprovision maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="d6cf7-105">Witaj kolejnych krokach objaśniono sposób przy użyciu programu PowerShell tooupload wirtualnego dysku twardego pliku tooa laboratorium dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-105">hello following steps walk you through using PowerShell tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="d6cf7-106">Po przesłaniu pliku wirtualnego dysku twardego hello [następne kroki sekcji](#next-steps) wymieniono niektóre artykuły, które przedstawiają sposób toocreate niestandardowego obrazu z hello przekazany plik VHD.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="d6cf7-107">Aby uzyskać więcej informacji o dyskach i wirtualne dyski twarde na platformie Azure, zobacz [o dyskach i wirtualne dyski twarde dla maszyn wirtualnych](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="d6cf7-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="d6cf7-108">Instrukcje krok po kroku</span><span class="sxs-lookup"><span data-stu-id="d6cf7-108">Step-by-step instructions</span></span>

<span data-ttu-id="d6cf7-109">Witaj następujące kroki przeszukiwania plików podczas przekazywania wirtualnego dysku twardego tooAzure DevTest Labs przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-109">hello following steps walk you through uploading a VHD file tooAzure DevTest Labs using PowerShell.</span></span> 

1. <span data-ttu-id="d6cf7-110">Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="d6cf7-110">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="d6cf7-111">Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-111">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="d6cf7-112">Z listy hello labs wybierz żądany laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-112">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="d6cf7-113">W bloku hello laboratorium, wybierz **konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-113">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="d6cf7-114">W laboratorium hello **konfiguracji** bloku, wybierz opcję **niestandardowych obrazów (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-114">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="d6cf7-115">Na powitania **niestandardowych obrazów** bloku, wybierz **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-115">On hello **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="d6cf7-116">Na powitania **obraz niestandardowy** bloku, wybierz opcję **wirtualnego dysku twardego**.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-116">On hello **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="d6cf7-117">Na powitania **wirtualnego dysku twardego** bloku, wybierz opcję **przekazania dysku VHD za pomocą programu PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-117">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Przekaż plik VHD za pomocą programu PowerShell](./media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. <span data-ttu-id="d6cf7-119">Na powitania **przekazywanie obrazu za pomocą programu PowerShell** bloku, Edytor tekstu tooa skryptu programu PowerShell hello wygenerowany kopiowania.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-119">On hello **Upload an image using PowerShell** blade, copy hello generated PowerShell script tooa text editor.</span></span>

1. <span data-ttu-id="d6cf7-120">Modyfikowanie hello **LocalFilePath** parametru hello **Add-AzureVhd** polecenia cmdlet toopoint toohello lokalizacja pliku wirtualnego dysku twardego, który chcesz tooupload hello.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-120">Modify hello **LocalFilePath** parameter of hello **Add-AzureVhd** cmdlet toopoint toohello location of hello VHD file you want tooupload.</span></span>

1. <span data-ttu-id="d6cf7-121">W wierszu polecenia programu PowerShell, uruchom hello **Add-AzureVhd** polecenia cmdlet (z hello zmodyfikowane **LocalFilePath** parametru).</span><span class="sxs-lookup"><span data-stu-id="d6cf7-121">At a PowerShell prompt, run hello **Add-AzureVhd** cmdlet (with hello modified **LocalFilePath** parameter).</span></span>

> [!WARNING] 
> 
> <span data-ttu-id="d6cf7-122">proces Hello przekazywania pliku wirtualnego dysku twardego może być długi w zależności od rozmiaru hello hello pliku wirtualnego dysku twardego i szybkość połączenia.</span><span class="sxs-lookup"><span data-stu-id="d6cf7-122">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6cf7-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d6cf7-123">Next steps</span></span>

- [<span data-ttu-id="d6cf7-124">Utworzyć obraz niestandardowy w usłudze Azure DevTest Labs z pliku VHD za pomocą hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d6cf7-124">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="d6cf7-125">Utworzyć obraz niestandardowy w usłudze Azure DevTest Labs z pliku VHD za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6cf7-125">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
