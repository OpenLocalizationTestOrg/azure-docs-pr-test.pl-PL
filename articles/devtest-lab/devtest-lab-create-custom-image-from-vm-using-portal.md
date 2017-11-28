---
title: aaaCreate niestandardowego obrazu z maszyny Wirtualnej Azure DevTest Labs | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate obraz niestandardowy w usłudze Azure DevTest Labs używającego zainicjowana VM hello portalu Azure"
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
ms.openlocfilehash: 7dccb79d3db4aae676c7bd2f6b800301210491e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vm"></a><span data-ttu-id="c7164-103">Tworzenie niestandardowego obrazu z maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c7164-103">Create a custom image from a VM</span></span>

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="c7164-104">Instrukcje krok po kroku</span><span class="sxs-lookup"><span data-stu-id="c7164-104">Step-by-step instructions</span></span>

<span data-ttu-id="c7164-105">Utworzyć niestandardowy obraz z elastycznie maszyny Wirtualnej, a następnie użyć tej toocreate niestandardowego obrazu identycznych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c7164-105">You can create a custom image from a provisioned VM, and afterwards use that custom image toocreate identical VMs.</span></span> <span data-ttu-id="c7164-106">Witaj, wykonaj czynności ilustrują sposób toocreate niestandardowego obrazu z maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="c7164-106">hello following steps illustrate how toocreate a custom image from a VM:</span></span>

1. <span data-ttu-id="c7164-107">Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="c7164-107">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="c7164-108">Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.</span><span class="sxs-lookup"><span data-stu-id="c7164-108">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="c7164-109">Z listy hello labs wybierz żądany laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="c7164-109">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="c7164-110">W bloku hello laboratorium, wybierz **Moje maszyny wirtualne**.</span><span class="sxs-lookup"><span data-stu-id="c7164-110">On hello lab's blade, select **My virtual machines**.</span></span>
 
1. <span data-ttu-id="c7164-111">Na powitania **Moje maszyny wirtualne** bloku, wybierz hello maszyny Wirtualnej, z którego mają zostać toocreate hello niestandardowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="c7164-111">On hello **My virtual machines** blade, select hello VM from which you want toocreate hello custom image.</span></span>

1. <span data-ttu-id="c7164-112">W bloku hello wirtualna wybierz **Tworzenie niestandardowego obrazu (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="c7164-112">On hello VM's blade, select **Create custom image (VHD)**.</span></span>

    ![Tworzenie niestandardowego obrazu elementu menu](./media/devtest-lab-create-template/create-custom-image.png)

1. <span data-ttu-id="c7164-114">Na powitania **Utwórz obraz** bloku, wprowadź nazwę i opis dla niestandardowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="c7164-114">On hello **Create image** blade, enter a name and description for your custom image.</span></span> <span data-ttu-id="c7164-115">Te informacje są wyświetlane na liście hello baz podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7164-115">This information is displayed in hello list of bases when you create a VM.</span></span>

    ![Tworzenie niestandardowego obrazu bloku](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. <span data-ttu-id="c7164-117">Określ, czy program sysprep zostało uruchomione na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c7164-117">Select whether sysprep was run on hello VM.</span></span> <span data-ttu-id="c7164-118">Jeśli hello sysprep nie zostało uruchomione na powitania maszyny Wirtualnej, określ, czy program sysprep uruchamiany po utworzeniu maszyny Wirtualnej z tego obrazu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="c7164-118">If hello sysprep was not run on hello VM, specify whether you want sysprep run when a VM is created from this custom image.</span></span>

1. <span data-ttu-id="c7164-119">Wybierz **OK** po toocreate Zakończono hello niestandardowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="c7164-119">Select **OK** when finished toocreate hello custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="c7164-120">Wpisy na blogu pokrewne</span><span class="sxs-lookup"><span data-stu-id="c7164-120">Related blog posts</span></span>

- [<span data-ttu-id="c7164-121">Niestandardowe obrazy lub formuł?</span><span class="sxs-lookup"><span data-stu-id="c7164-121">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="c7164-122">Kopiowanie obrazów niestandardowych między Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="c7164-122">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="c7164-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c7164-123">Next steps</span></span>

- [<span data-ttu-id="c7164-124">Dodawanie laboratorium tooyour maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c7164-124">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
