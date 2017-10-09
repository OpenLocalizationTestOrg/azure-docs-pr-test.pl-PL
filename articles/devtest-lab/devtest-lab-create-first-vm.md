---
title: "aaaCreate pierwszej maszyny Wirtualnej w laboratorium w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Twojego pierwszego maszynę wirtualną w laboratorium w usłudze Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: fbc5a438-6e02-4952-b654-b8fa7322ae5f
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/24/2017
ms.author: tarcher
ms.openlocfilehash: 4c3257efca9be6fdd190eaac1db731464e07fcfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="dc8ac-103">Tworzenie pierwszej maszyny Wirtualnej w laboratorium w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="dc8ac-103">Create your first VM in a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="dc8ac-104">Gdy początkowo dostęp DevTest Labs i zechcesz toocreate pierwszej maszyny Wirtualnej, możesz będzie prawdopodobnie to zrobić za pomocą wstępnie załadowane [obrazu z witryny marketplace podstawowej](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="dc8ac-104">When you initially access DevTest Labs and want toocreate your first VM, you will likely do so using a pre-loaded [base marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="dc8ac-105">Później również będziesz w stanie toochoose z [niestandardowego obrazu oraz formułę](devtest-lab-add-vm.md) podczas tworzenia więcej maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="dc8ac-105">Later on, you'll also be able toochoose from a [custom image and a formula](devtest-lab-add-vm.md) when creating more VMs.</span></span> 

<span data-ttu-id="dc8ac-106">Ten samouczek przedstawia przy użyciu hello Azure tooadd portalu pierwszy laboratorium tooa maszyny Wirtualnej w usłudze DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="dc8ac-106">This tutorial walks you through using hello Azure portal tooadd your first VM tooa lab in DevTest Labs.</span></span>

## <a name="steps-tooadd-your-first-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="dc8ac-107">Kroki tooadd pierwszy laboratorium tooa maszyny Wirtualnej w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="dc8ac-107">Steps tooadd your first VM tooa lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="dc8ac-108">Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="dc8ac-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="dc8ac-109">Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.</span><span class="sxs-lookup"><span data-stu-id="dc8ac-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="dc8ac-110">Z listy hello labs wybierz laboratorium hello, w której ma zostać hello toocreate maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dc8ac-110">From hello list of labs, select hello lab in which you want toocreate hello VM.</span></span>  
1. <span data-ttu-id="dc8ac-111">W laboratorium hello **omówienie** bloku, wybierz opcję **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="dc8ac-111">On hello lab's **Overview** blade, select **+ Add**.</span></span>  

    ![Dodawanie przycisku maszyny Wirtualnej](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="dc8ac-113">Na powitania **wybierz podstawowej** bloku, wybierz obraz marketplace hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dc8ac-113">On hello **Choose a base** blade, select a marketplace image for hello VM.</span></span>
1. <span data-ttu-id="dc8ac-114">Na powitania **maszyny wirtualnej** bloku, wprowadź nazwę dla nowej maszyny wirtualnej hello w hello **nazwę maszyny wirtualnej** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="dc8ac-114">On hello **Virtual machine** blade, enter a name for hello new virtual machine in hello **Virtual machine name** text box.</span></span>

    ![Bloku maszyny Wirtualnej laboratorium](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. <span data-ttu-id="dc8ac-116">Wprowadź **nazwy użytkownika** udzieleniu uprawnień administratora na maszynie wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="dc8ac-116">Enter a **User Name** that is granted administrator privileges on hello virtual machine.</span></span>  
1. <span data-ttu-id="dc8ac-117">Wprowadź hasło w polu tekstowym hello etykietą **wpisz wartość**.</span><span class="sxs-lookup"><span data-stu-id="dc8ac-117">Enter a password in hello text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="dc8ac-118">Witaj **typu dysku maszyny wirtualnej** Określa, który typ dysku magazynu jest dozwolony dla hello maszyn wirtualnych w laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="dc8ac-118">hello **Virtual machine disk type** determines which storage disk type is allowed for hello virtual machines in hello lab.</span></span>
1. <span data-ttu-id="dc8ac-119">Wybierz **rozmiar maszyny wirtualnej** i wybierz jedną z hello wstępnie zdefiniowane elementy, które określić hello rdzeni procesora, rozmiar pamięci RAM i rozmiar dysku twardego hello hello toocreate maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dc8ac-119">Select **Virtual machine size** and select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span>
1. <span data-ttu-id="dc8ac-120">Wybierz **artefakty** — z listy hello artefaktów — wybierz i skonfiguruj artefakty hello, które mają tooadd toohello podstawowy obraz.</span><span class="sxs-lookup"><span data-stu-id="dc8ac-120">Select **Artifacts** and - from hello list of artifacts - select and configure hello artifacts that you want tooadd toohello base image.</span></span>
    <span data-ttu-id="dc8ac-121">**Uwaga:** nowe Labs tooDevTest lub konfigurowanie artefaktów, zobacz toohello [Dodawanie istniejących tooa artefaktu maszyny Wirtualnej](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) sekcji, a następnie wróć tutaj po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="dc8ac-121">**Note:** If you're new tooDevTest Labs or configuring artifacts, refer toohello [Add an existing artifact tooa VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="dc8ac-122">Wybierz **Utwórz** tooadd hello określony laboratorium toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dc8ac-122">Select **Create** tooadd hello specified VM toohello lab.</span></span>

   <span data-ttu-id="dc8ac-123">Blok laboratorium Hello Wyświetla stan hello tworzenie hello VM - najpierw jako **tworzenie**, następnie jako **systemem** po hello maszyna wirtualna została uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="dc8ac-123">hello lab blade displays hello status of hello VM's creation - first as **Creating**, then as **Running** after hello VM has been started.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc8ac-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dc8ac-124">Next steps</span></span>
* <span data-ttu-id="dc8ac-125">Raz hello maszyna wirtualna została utworzona, można połączyć toohello maszyny Wirtualnej, wybierając **Connect** w bloku hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dc8ac-125">Once hello VM has been created, you can connect toohello VM by selecting **Connect** on hello VM's blade.</span></span>
* <span data-ttu-id="dc8ac-126">Zapoznaj się z [Dodawanie maszyny Wirtualnej laboratorium tooa](devtest-lab-add-vm.md) na pełniejsze informacje dotyczące dodawania kolejnych maszyn wirtualnych w laboratorium.</span><span class="sxs-lookup"><span data-stu-id="dc8ac-126">Check out [Add a VM tooa lab](devtest-lab-add-vm.md) for more complete info about adding subsequent VMs in your lab.</span></span>
* <span data-ttu-id="dc8ac-127">Eksploruj hello [galerię szablonów DevTest Labs Azure Resource Manager — Szybki Start](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span><span class="sxs-lookup"><span data-stu-id="dc8ac-127">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span></span>
