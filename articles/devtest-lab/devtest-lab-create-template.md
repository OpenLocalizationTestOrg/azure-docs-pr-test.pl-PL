---
title: Tworzenie obrazu niestandardowego Azure DevTest Labs na podstawie pliku VHD | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak utworzyć obraz niestandardowy w usłudze Azure DevTest Labs z pliku VHD za pomocą portalu Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: b795bc61-7c28-40e6-82fc-96d629ee0568
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 9983ea9b847f44ed18a6169a4bdb224b63626a64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="139e2-103">Tworzenie niestandardowego obrazu z pliku VHD</span><span class="sxs-lookup"><span data-stu-id="139e2-103">Create a custom image from a VHD file</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="139e2-104">Instrukcje krok po kroku</span><span class="sxs-lookup"><span data-stu-id="139e2-104">Step-by-step instructions</span></span>

<span data-ttu-id="139e2-105">W poniższych krokach objaśniono przez proces tworzenia niestandardowego obrazu z pliku VHD za pomocą portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="139e2-105">The following steps walk you through creating a custom image from a VHD file using the Azure portal:</span></span>

1. <span data-ttu-id="139e2-106">Zaloguj się w witrynie [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="139e2-106">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="139e2-107">Wybierz pozycję **Więcej usług**, a następnie z listy wybierz pozycję **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="139e2-107">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="139e2-108">Z listy labs wybierz żądany laboratorium.</span><span class="sxs-lookup"><span data-stu-id="139e2-108">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="139e2-109">W bloku laboratorium, wybierz **konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="139e2-109">On the lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="139e2-110">W środowisku laboratoryjnym **konfiguracji** bloku, wybierz opcję **niestandardowych obrazów (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="139e2-110">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="139e2-111">Na **niestandardowych obrazów** bloku, wybierz opcję **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="139e2-111">On the **Custom images** blade, select **+Add**.</span></span>

    ![Dodaj niestandardowy obraz](./media/devtest-lab-create-template/add-custom-image.png)

1. <span data-ttu-id="139e2-113">Wprowadź nazwę niestandardowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="139e2-113">Enter the name of the custom image.</span></span> <span data-ttu-id="139e2-114">Ta nazwa będzie wyświetlana na liście podstawowej obrazów, podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="139e2-114">This name is displayed in the list of base images when creating a VM.</span></span>

1. <span data-ttu-id="139e2-115">Wprowadź opis niestandardowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="139e2-115">Enter the description of the custom image.</span></span> <span data-ttu-id="139e2-116">Ten opis jest wyświetlany na liście obrazów podstawowej podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="139e2-116">This description is displayed in the list of base images when creating a VM.</span></span>

1. <span data-ttu-id="139e2-117">Wybierz **wirtualnego dysku twardego**.</span><span class="sxs-lookup"><span data-stu-id="139e2-117">Select **VHD**.</span></span>

1. <span data-ttu-id="139e2-118">Z **wirtualnego dysku twardego** bloku, wybierz żądany plik wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="139e2-118">From the **VHD** blade, select the desired VHD file.</span></span>

1. <span data-ttu-id="139e2-119">Wybierz **OK** zamknąć **wirtualnego dysku twardego** bloku.</span><span class="sxs-lookup"><span data-stu-id="139e2-119">Select **OK** to close the **VHD** blade.</span></span>

1. <span data-ttu-id="139e2-120">Wybierz **Konfiguracja systemu operacyjnego**.</span><span class="sxs-lookup"><span data-stu-id="139e2-120">Select **OS configuration**.</span></span>

1. <span data-ttu-id="139e2-121">Na **Konfiguracja systemu operacyjnego** , a następnie wybierz opcję **Windows** lub **Linux**.</span><span class="sxs-lookup"><span data-stu-id="139e2-121">On the **OS configuration** tab, select either **Windows** or **Linux**.</span></span>

1. <span data-ttu-id="139e2-122">Jeśli **Windows** jest zaznaczone, określ za pomocą pola wyboru czy *Sysprep* zostało uruchomione na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="139e2-122">If **Windows** is selected, specify via the checkbox whether *Sysprep* has been run on the machine.</span></span> 

1. <span data-ttu-id="139e2-123">Wybierz **OK** zamknąć **Konfiguracja systemu operacyjnego** bloku.</span><span class="sxs-lookup"><span data-stu-id="139e2-123">Select **OK** to close the **OS configuration** blade.</span></span>

1. <span data-ttu-id="139e2-124">Wybierz **OK** można utworzyć niestandardowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="139e2-124">Select **OK** to create the custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="139e2-125">Wpisy na blogu pokrewne</span><span class="sxs-lookup"><span data-stu-id="139e2-125">Related blog posts</span></span>

- [<span data-ttu-id="139e2-126">Niestandardowe obrazy lub formuł?</span><span class="sxs-lookup"><span data-stu-id="139e2-126">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="139e2-127">Kopiowanie obrazów niestandardowych między Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="139e2-127">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="139e2-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="139e2-128">Next steps</span></span>

- [<span data-ttu-id="139e2-129">Dodaj Maszynę wirtualną do laboratorium</span><span class="sxs-lookup"><span data-stu-id="139e2-129">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
