---
title: "Tworzenie pierwszej maszyny Wirtualnej w laboratorium w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć pierwszy maszynę wirtualną w laboratorium w usłudze Azure DevTest Labs"
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
ms.openlocfilehash: aa6b60b799e1e98815cf288d5612f98cd77cc00e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="ac814-103">Tworzenie pierwszej maszyny Wirtualnej w laboratorium w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="ac814-103">Create your first VM in a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="ac814-104">Przy pierwszym dostępu DevTest Labs i chcesz utworzyć pierwszy maszyny Wirtualnej, możesz będzie prawdopodobnie to zrobić za pomocą wstępnie załadowane [obrazu z witryny marketplace podstawowej](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="ac814-104">When you initially access DevTest Labs and want to create your first VM, you will likely do so using a pre-loaded [base marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="ac814-105">Później również będzie można wybrać [niestandardowego obrazu oraz formułę](devtest-lab-add-vm.md) podczas tworzenia więcej maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ac814-105">Later on, you'll also be able to choose from a [custom image and a formula](devtest-lab-add-vm.md) when creating more VMs.</span></span> 

<span data-ttu-id="ac814-106">Ten samouczek przeprowadzi Cię przez dodawanie pierwszej maszyny Wirtualnej do laboratorium w usłudze DevTest Labs przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ac814-106">This tutorial walks you through using the Azure portal to add your first VM to a lab in DevTest Labs.</span></span>

## <a name="steps-to-add-your-first-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="ac814-107">Kroki, aby dodać pierwszy maszyny Wirtualnej do laboratorium w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="ac814-107">Steps to add your first VM to a lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="ac814-108">Zaloguj się w witrynie [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="ac814-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="ac814-109">Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy.</span><span class="sxs-lookup"><span data-stu-id="ac814-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="ac814-110">Z listy labs wybierz laboratorium, w którym chcesz utworzyć maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="ac814-110">From the list of labs, select the lab in which you want to create the VM.</span></span>  
1. <span data-ttu-id="ac814-111">W laboratorium **omówienie** bloku, wybierz opcję **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="ac814-111">On the lab's **Overview** blade, select **+ Add**.</span></span>  

    ![Dodawanie przycisku maszyny Wirtualnej](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="ac814-113">Na **wybierz podstawowej** bloku, wybierz pozycję marketplace obrazu dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac814-113">On the **Choose a base** blade, select a marketplace image for the VM.</span></span>
1. <span data-ttu-id="ac814-114">Na **maszyny wirtualnej** bloku, wprowadź nazwę dla nowej maszyny wirtualnej w **nazwę maszyny wirtualnej** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="ac814-114">On the **Virtual machine** blade, enter a name for the new virtual machine in the **Virtual machine name** text box.</span></span>

    ![Bloku maszyny Wirtualnej laboratorium](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. <span data-ttu-id="ac814-116">Wprowadź **nazwy użytkownika** udzieleniu uprawnień administratora na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac814-116">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span></span>  
1. <span data-ttu-id="ac814-117">Wprowadź hasło w polu tekstowym etykietą **wpisz wartość**.</span><span class="sxs-lookup"><span data-stu-id="ac814-117">Enter a password in the text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="ac814-118">**Typu dysku maszyny wirtualnej** Określa, który typ dysku magazynu jest dozwolony dla maszyn wirtualnych w laboratorium.</span><span class="sxs-lookup"><span data-stu-id="ac814-118">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span></span>
1. <span data-ttu-id="ac814-119">Wybierz **rozmiar maszyny wirtualnej** i wybierz jedną z wstępnie zdefiniowane elementy, które Określ rdzeni procesora, rozmiar pamięci RAM i rozmiar dysku twardego maszyny wirtualnej do utworzenia.</span><span class="sxs-lookup"><span data-stu-id="ac814-119">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span>
1. <span data-ttu-id="ac814-120">Wybierz **artefakty** a — z listy artefakty — wybierz i skonfiguruj artefaktów, które chcesz dodać do obrazu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="ac814-120">Select **Artifacts** and - from the list of artifacts - select and configure the artifacts that you want to add to the base image.</span></span>
    <span data-ttu-id="ac814-121">**Uwaga:** Jeśli nowych użytkowników programu DevTest Labs lub konfigurowanie artefaktów, zapoznaj się [Dodaj istniejący artefakt do maszyny Wirtualnej](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) sekcji, a następnie wróć tutaj po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="ac814-121">**Note:** If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="ac814-122">Wybierz **Utwórz** dodać określoną maszynę Wirtualną do laboratorium.</span><span class="sxs-lookup"><span data-stu-id="ac814-122">Select **Create** to add the specified VM to the lab.</span></span>

   <span data-ttu-id="ac814-123">Blok laboratorium Wyświetla stan tworzenia maszyny Wirtualnej — najpierw jako **tworzenie**, następnie jako **systemem** po uruchomieniu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac814-123">The lab blade displays the status of the VM's creation - first as **Creating**, then as **Running** after the VM has been started.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac814-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ac814-124">Next steps</span></span>
* <span data-ttu-id="ac814-125">Po utworzeniu maszyny Wirtualnej można Połącz się z maszyną Wirtualną, wybierając **Connect** w bloku maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac814-125">Once the VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span></span>
* <span data-ttu-id="ac814-126">Zapoznaj się z [dodać maszyny Wirtualnej do laboratorium](devtest-lab-add-vm.md) na pełniejsze informacje dotyczące dodawania kolejnych maszyn wirtualnych w laboratorium.</span><span class="sxs-lookup"><span data-stu-id="ac814-126">Check out [Add a VM to a lab](devtest-lab-add-vm.md) for more complete info about adding subsequent VMs in your lab.</span></span>
* <span data-ttu-id="ac814-127">Eksploruj [galerię szablonów DevTest Labs Azure Resource Manager — Szybki Start](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span><span class="sxs-lookup"><span data-stu-id="ac814-127">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span></span>
