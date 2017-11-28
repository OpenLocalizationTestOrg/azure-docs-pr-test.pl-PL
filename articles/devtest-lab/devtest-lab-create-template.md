---
title: aaaCreate niestandardowego obrazu z pliku VHD Azure DevTest Labs | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate obraz niestandardowy w usłudze Azure DevTest Labs od pliku wirtualnego dysku twardego za pomocą hello portalu Azure"
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
ms.openlocfilehash: 80af8ea1cb72380f868df0a76c4a0dcd92e63cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="a1a47-103">Tworzenie niestandardowego obrazu z pliku VHD</span><span class="sxs-lookup"><span data-stu-id="a1a47-103">Create a custom image from a VHD file</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="a1a47-104">Instrukcje krok po kroku</span><span class="sxs-lookup"><span data-stu-id="a1a47-104">Step-by-step instructions</span></span>

<span data-ttu-id="a1a47-105">Witaj następujących krokach objaśniono sposób tworzenia niestandardowego obrazu z pliku VHD za pomocą hello portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="a1a47-105">hello following steps walk you through creating a custom image from a VHD file using hello Azure portal:</span></span>

1. <span data-ttu-id="a1a47-106">Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="a1a47-106">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="a1a47-107">Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.</span><span class="sxs-lookup"><span data-stu-id="a1a47-107">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="a1a47-108">Z listy hello labs wybierz żądany laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="a1a47-108">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="a1a47-109">W bloku hello laboratorium, wybierz **konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="a1a47-109">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="a1a47-110">W laboratorium hello **konfiguracji** bloku, wybierz opcję **niestandardowych obrazów (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="a1a47-110">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="a1a47-111">Na powitania **niestandardowych obrazów** bloku, wybierz opcję **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a1a47-111">On hello **Custom images** blade, select **+Add**.</span></span>

    ![Dodaj niestandardowy obraz](./media/devtest-lab-create-template/add-custom-image.png)

1. <span data-ttu-id="a1a47-113">Wprowadź nazwę hello hello niestandardowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="a1a47-113">Enter hello name of hello custom image.</span></span> <span data-ttu-id="a1a47-114">Ta nazwa będzie wyświetlana na liście hello podstawowej obrazów, podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a1a47-114">This name is displayed in hello list of base images when creating a VM.</span></span>

1. <span data-ttu-id="a1a47-115">Wprowadź opis hello hello niestandardowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="a1a47-115">Enter hello description of hello custom image.</span></span> <span data-ttu-id="a1a47-116">Ten opis jest wyświetlany w hello listy obrazów podstawowej podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a1a47-116">This description is displayed in hello list of base images when creating a VM.</span></span>

1. <span data-ttu-id="a1a47-117">Wybierz **wirtualnego dysku twardego**.</span><span class="sxs-lookup"><span data-stu-id="a1a47-117">Select **VHD**.</span></span>

1. <span data-ttu-id="a1a47-118">Z hello **wirtualnego dysku twardego** bloku, hello wybierz żądany plik wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="a1a47-118">From hello **VHD** blade, select hello desired VHD file.</span></span>

1. <span data-ttu-id="a1a47-119">Wybierz **OK** tooclose hello **wirtualnego dysku twardego** bloku.</span><span class="sxs-lookup"><span data-stu-id="a1a47-119">Select **OK** tooclose hello **VHD** blade.</span></span>

1. <span data-ttu-id="a1a47-120">Wybierz **Konfiguracja systemu operacyjnego**.</span><span class="sxs-lookup"><span data-stu-id="a1a47-120">Select **OS configuration**.</span></span>

1. <span data-ttu-id="a1a47-121">Na powitania **Konfiguracja systemu operacyjnego** , a następnie wybierz opcję **Windows** lub **Linux**.</span><span class="sxs-lookup"><span data-stu-id="a1a47-121">On hello **OS configuration** tab, select either **Windows** or **Linux**.</span></span>

1. <span data-ttu-id="a1a47-122">Jeśli **Windows** jest zaznaczone, określ za pomocą pola wyboru hello czy *Sysprep* zostało uruchomione na maszynie hello.</span><span class="sxs-lookup"><span data-stu-id="a1a47-122">If **Windows** is selected, specify via hello checkbox whether *Sysprep* has been run on hello machine.</span></span> 

1. <span data-ttu-id="a1a47-123">Wybierz **OK** tooclose hello **Konfiguracja systemu operacyjnego** bloku.</span><span class="sxs-lookup"><span data-stu-id="a1a47-123">Select **OK** tooclose hello **OS configuration** blade.</span></span>

1. <span data-ttu-id="a1a47-124">Wybierz **OK** toocreate hello niestandardowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="a1a47-124">Select **OK** toocreate hello custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="a1a47-125">Wpisy na blogu pokrewne</span><span class="sxs-lookup"><span data-stu-id="a1a47-125">Related blog posts</span></span>

- [<span data-ttu-id="a1a47-126">Niestandardowe obrazy lub formuł?</span><span class="sxs-lookup"><span data-stu-id="a1a47-126">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="a1a47-127">Kopiowanie obrazów niestandardowych między Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a1a47-127">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="a1a47-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a1a47-128">Next steps</span></span>

- [<span data-ttu-id="a1a47-129">Dodawanie laboratorium tooyour maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a1a47-129">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
