---
title: Tworzenie obrazu niestandardowego Azure DevTest Labs na podstawie maszyny Wirtualnej | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak utworzyć obraz niestandardowy w usłudze Azure DevTest Labs elastycznie maszyny wirtualnej przy użyciu portalu Azure"
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
ms.openlocfilehash: 9d2dcf7164985508d691e8a0c123efaf3b8aa19a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vm"></a><span data-ttu-id="b7ba6-103">Tworzenie niestandardowego obrazu z maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b7ba6-103">Create a custom image from a VM</span></span>

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="b7ba6-104">Instrukcje krok po kroku</span><span class="sxs-lookup"><span data-stu-id="b7ba6-104">Step-by-step instructions</span></span>

<span data-ttu-id="b7ba6-105">Można utworzyć niestandardowy obraz z elastycznie maszyny Wirtualnej, a później użyć niestandardowego obrazu do utworzenia identycznych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="b7ba6-105">You can create a custom image from a provisioned VM, and afterwards use that custom image to create identical VMs.</span></span> <span data-ttu-id="b7ba6-106">Poniższe kroki pokazano, jak utworzyć obraz niestandardowy z maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="b7ba6-106">The following steps illustrate how to create a custom image from a VM:</span></span>

1. <span data-ttu-id="b7ba6-107">Zaloguj się w witrynie [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="b7ba6-107">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="b7ba6-108">Wybierz pozycję **Więcej usług**, a następnie z listy wybierz pozycję **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="b7ba6-108">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="b7ba6-109">Z listy labs wybierz żądany laboratorium.</span><span class="sxs-lookup"><span data-stu-id="b7ba6-109">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="b7ba6-110">W bloku laboratorium, wybierz **Moje maszyny wirtualne**.</span><span class="sxs-lookup"><span data-stu-id="b7ba6-110">On the lab's blade, select **My virtual machines**.</span></span>
 
1. <span data-ttu-id="b7ba6-111">Na **Moje maszyny wirtualne** bloku, wybierz maszynę Wirtualną, z którego chcesz utworzyć niestandardowy obraz.</span><span class="sxs-lookup"><span data-stu-id="b7ba6-111">On the **My virtual machines** blade, select the VM from which you want to create the custom image.</span></span>

1. <span data-ttu-id="b7ba6-112">W bloku maszyny Wirtualnej, wybierz **Tworzenie niestandardowego obrazu (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="b7ba6-112">On the VM's blade, select **Create custom image (VHD)**.</span></span>

    ![Tworzenie niestandardowego obrazu elementu menu](./media/devtest-lab-create-template/create-custom-image.png)

1. <span data-ttu-id="b7ba6-114">Na **Utwórz obraz** bloku, wprowadź nazwę i opis dla niestandardowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="b7ba6-114">On the **Create image** blade, enter a name and description for your custom image.</span></span> <span data-ttu-id="b7ba6-115">Te informacje są wyświetlane na liście klas podstawowych, podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b7ba6-115">This information is displayed in the list of bases when you create a VM.</span></span>

    ![Tworzenie niestandardowego obrazu bloku](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. <span data-ttu-id="b7ba6-117">Określ, czy uruchomiono program sysprep na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b7ba6-117">Select whether sysprep was run on the VM.</span></span> <span data-ttu-id="b7ba6-118">Jeśli nie uruchomiono programu sysprep na maszynie Wirtualnej, określ, czy uruchamiany po utworzeniu maszyny Wirtualnej z tego obrazu niestandardowego narzędzia sysprep.</span><span class="sxs-lookup"><span data-stu-id="b7ba6-118">If the sysprep was not run on the VM, specify whether you want sysprep run when a VM is created from this custom image.</span></span>

1. <span data-ttu-id="b7ba6-119">Wybierz **OK** po zakończeniu można utworzyć niestandardowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="b7ba6-119">Select **OK** when finished to create the custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="b7ba6-120">Wpisy na blogu pokrewne</span><span class="sxs-lookup"><span data-stu-id="b7ba6-120">Related blog posts</span></span>

- [<span data-ttu-id="b7ba6-121">Niestandardowe obrazy lub formuł?</span><span class="sxs-lookup"><span data-stu-id="b7ba6-121">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="b7ba6-122">Kopiowanie obrazów niestandardowych między Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b7ba6-122">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="b7ba6-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b7ba6-123">Next steps</span></span>

- [<span data-ttu-id="b7ba6-124">Dodaj Maszynę wirtualną do laboratorium</span><span class="sxs-lookup"><span data-stu-id="b7ba6-124">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
