---
title: "ustawienia obrazu portalu Azure Marketplace aaaConfigure w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Konfigurowanie obrazów Azure Marketplace, których można użyć w przypadku tworzenia maszyny Wirtualnej w usłudze Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 804c6af2-17e9-4320-af3a-f454bd398379
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: bb4b7f1c0cbe967bee724f7ee20f64f8c4ea58ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a><span data-ttu-id="fe0e9-103">Skonfiguruj ustawienia obrazu portalu Azure Marketplace w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="fe0e9-103">Configure Azure Marketplace image settings in Azure DevTest Labs</span></span>
<span data-ttu-id="fe0e9-104">DevTest Labs obsługuje tworzenia maszyn wirtualnych, oparte na obrazach portalu Azure Marketplace w zależności od sposobu konfiguracji portalu Azure Marketplace toobe obrazy używane w laboratorium.</span><span class="sxs-lookup"><span data-stu-id="fe0e9-104">DevTest Labs supports creating VMs based on Azure Marketplace images depending on how you have configured Azure Marketplace images toobe used in your lab.</span></span> <span data-ttu-id="fe0e9-105">W tym artykule opisano sposób toospecify, którego, portalu Azure Marketplace obrazy mogą być używane podczas tworzenia maszyn wirtualnych w laboratorium.</span><span class="sxs-lookup"><span data-stu-id="fe0e9-105">This article shows you how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span> <span data-ttu-id="fe0e9-106">Dzięki temu, że zespół ma tylko dostępu toohello Marketplace obrazów, które są im potrzebne.</span><span class="sxs-lookup"><span data-stu-id="fe0e9-106">This ensures that your team only has access toohello Marketplace images they need.</span></span> 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a><span data-ttu-id="fe0e9-107">Wybierz obrazy portalu Azure Marketplace, które są dozwolone podczas tworzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="fe0e9-107">Select which Azure Marketplace images are allowed when creating a VM</span></span>
1. <span data-ttu-id="fe0e9-108">Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="fe0e9-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="fe0e9-109">Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.</span><span class="sxs-lookup"><span data-stu-id="fe0e9-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="fe0e9-110">Z listy hello labs wybierz żądany laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="fe0e9-110">From hello list of labs, select hello desired lab.</span></span> 
4. <span data-ttu-id="fe0e9-111">W bloku hello laboratorium, wybierz **konfiguracji i zasadach**.</span><span class="sxs-lookup"><span data-stu-id="fe0e9-111">On hello lab's blade, select **Configuration and policies**.</span></span>
5. <span data-ttu-id="fe0e9-112">W laboratorium w **konfiguracji i zasadach** bloku w obszarze **baz maszyn wirtualnych**, wybierz pozycję **obrazów Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="fe0e9-112">On lab's **Configuration and policies** blade under **Virtual Machine Bases**, select **Marketplace images**.</span></span>
6. <span data-ttu-id="fe0e9-113">Określ, czy się, że wszystkie hello kwalifikowaną toobe obrazów Azure Marketplace dostępne do użycia jako baza dla nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fe0e9-113">Specify whether you want all hello qualified Azure Marketplace images toobe available for use as a base of a new VM.</span></span> <span data-ttu-id="fe0e9-114">W przypadku wybrania **tak**, następnie wszystkie obrazy portalu Azure Marketplace hello spełniające wszystkie hello następujące kryteria są dozwolone w laboratorium hello:</span><span class="sxs-lookup"><span data-stu-id="fe0e9-114">If you select **Yes**, then all hello Azure Marketplace images that meet all hello following criteria are allowed in hello lab:</span></span>
   
   * <span data-ttu-id="fe0e9-115">Obraz powitania tworzy jednej maszyny Wirtualnej, **i**</span><span class="sxs-lookup"><span data-stu-id="fe0e9-115">hello image creates a single VM, **and**</span></span>
   * <span data-ttu-id="fe0e9-116">Obraz powitania używa usługi Azure Resource Manager tooprovision maszyn wirtualnych, **i**</span><span class="sxs-lookup"><span data-stu-id="fe0e9-116">hello image uses Azure Resource Manager tooprovision VMs, **and**</span></span>
   * <span data-ttu-id="fe0e9-117">Obraz powitania nie wymaga zakup planu licencjonowania bardzo</span><span class="sxs-lookup"><span data-stu-id="fe0e9-117">hello image doesn't require purchasing an extra licensing plan</span></span>
     
    <span data-ttu-id="fe0e9-118">Jeśli nie toobe obrazów dozwolone, lub ma toospecify obrazów, które mogą być używane, wybierz **nr**.</span><span class="sxs-lookup"><span data-stu-id="fe0e9-118">If you want no images toobe allowed, or you want toospecify which images can be used, select **No**.</span></span>
     
     ![Opcja tooallow wszystkie toobe obrazów w witrynie Marketplace używany jako obrazy podstawowe dla maszyn wirtualnych](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. <span data-ttu-id="fe0e9-120">W przypadku wybrania **nr** toohello poprzedniego kroku, hello **dozwolone obrazów/wybierz wszystkie** pole wyboru jest włączone.</span><span class="sxs-lookup"><span data-stu-id="fe0e9-120">If you select **No** toohello previous step, hello **Allowed images/Select all** checkbox is enabled.</span></span> 
   <span data-ttu-id="fe0e9-121">Możesz użyć tej opcji wraz z wybierz tooquickly pole wyszukiwania hello lub usuń zaznaczenie wszystkich elementów hello wyświetlane na liście hello.</span><span class="sxs-lookup"><span data-stu-id="fe0e9-121">You can use this option together with hello search box tooquickly select or deselect all hello items displayed in hello list.</span></span>
   * <span data-ttu-id="fe0e9-122">Wybierz hello Azure Marketplace obrazy tooallow dla tworzenia maszyny Wirtualnej pojedynczo, zaznaczając wyboru odpowiednich każdego obrazu.</span><span class="sxs-lookup"><span data-stu-id="fe0e9-122">Select hello Azure Marketplace images you want tooallow for VM creation individually by checking each image's corresponding checkbox.</span></span>
   * <span data-ttu-id="fe0e9-123">Wybierz nic z listy hello, jeśli nie chcesz tooallow żadnych portalu Azure Marketplace toobe obrazy używane w laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="fe0e9-123">Select nothing from hello list if you don't want tooallow any Azure Marketplace images toobe used in hello lab.</span></span>
   
    ![Można określić, które obrazy portalu Azure Marketplace może służyć jako podstawowy obrazów maszyn wirtualnych](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="fe0e9-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fe0e9-125">Next steps</span></span>
<span data-ttu-id="fe0e9-126">Po skonfigurowaniu, jak obrazy portalu Azure Marketplace są dozwolone podczas tworzenia maszyny Wirtualnej, następnym krokiem hello jest zbyt[Dodawanie maszyny Wirtualnej laboratorium tooyour](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="fe0e9-126">Once you have configured how Azure Marketplace images are allowed when creating a VM, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

